## 新旧支付系统兼容

<font color="#95b3d7">背景</font>：
老系统对接了 “支付宝旧版 SDK”（接口：`alipayOldPay(String orderId, double amount)`），新需求要对接 “支付宝新版 SDK”（接口：`newAlipayPay(OrderDTO orderDTO)`）和 “微信支付 SDK”（接口：`wechatPay(String outTradeNo, BigDecimal totalFee)`），但上层业务代码想统一调用`pay(Order order)`，不想为不同支付方式写不同逻辑。

<font color="#95b3d7">代码</font>：
```java
// 1. 定义统一的目标接口（上层业务想调用的接口）
public interface PaymentAdapter {
    // 统一支付方法
    String pay(Order order);
}

// 2. 老系统的支付宝旧版SDK（不能修改的老代码）
public class AlipayOldSDK {
    // 旧接口：参数是订单ID+金额（double）
    public String alipayOldPay(String orderId, double amount) {
        return "支付宝旧版支付成功，订单号：" + orderId + "，金额：" + amount + "元";
    }
}

// 3. 支付宝新版SDK（第三方新接口）
public class AlipayNewSDK {
    // 新接口：参数是OrderDTO对象
    public String newAlipayPay(OrderDTO orderDTO) {
        return "支付宝新版支付成功，订单号：" + orderDTO.getOrderId() + "，金额：" + orderDTO.getAmount() + "元";
    }
}

// 4. 微信支付SDK（第三方接口）
public class WechatPaySDK {
    // 微信接口：参数是商户订单号+金额（BigDecimal）
    public String wechatPay(String outTradeNo, BigDecimal totalFee) {
        return "微信支付成功，商户订单号：" + outTradeNo + "，金额：" + totalFee + "元";
    }
}

// 5. 适配类1：支付宝旧版适配器
public class AlipayOldAdapter implements PaymentAdapter {
    // 持有被适配的老SDK对象
    private AlipayOldSDK alipayOldSDK;

    public AlipayOldAdapter(AlipayOldSDK alipayOldSDK) {
        this.alipayOldSDK = alipayOldSDK;
    }

    @Override
    public String pay(Order order) {
        // 适配逻辑：将Order对象转换成老SDK需要的参数
        String orderId = order.getOrderId();
        double amount = order.getAmount().doubleValue();
        // 调用老SDK的接口
        return alipayOldSDK.alipayOldPay(orderId, amount);
    }
}

// 6. 适配类2：支付宝新版适配器
public class AlipayNewAdapter implements PaymentAdapter {
    private AlipayNewSDK alipayNewSDK;

    public AlipayNewAdapter(AlipayNewSDK alipayNewSDK) {
        this.alipayNewSDK = alipayNewSDK;
    }

    @Override
    public String pay(Order order) {
        // 适配逻辑：将Order转换成新版SDK需要的OrderDTO
        OrderDTO orderDTO = new OrderDTO();
        orderDTO.setOrderId(order.getOrderId());
        orderDTO.setAmount(order.getAmount());
        orderDTO.setUserId(order.getUserId());
        // 调用新版SDK的接口
        return alipayNewSDK.newAlipayPay(orderDTO);
    }
}

// 7. 适配类3：微信支付适配器
public class WechatPayAdapter implements PaymentAdapter {
    private WechatPaySDK wechatPaySDK;

    public WechatPayAdapter(WechatPaySDK wechatPaySDK) {
        this.wechatPaySDK = wechatPaySDK;
    }

    @Override
    public String pay(Order order) {
        // 适配逻辑：将Order转换成微信SDK需要的参数
        String outTradeNo = "WX_" + order.getOrderId(); // 拼接微信商户订单号
        BigDecimal totalFee = order.getAmount();
        // 调用微信SDK的接口
        return wechatPaySDK.wechatPay(outTradeNo, totalFee);
    }
}

// 辅助类定义
class Order {
    private String orderId;
    private BigDecimal amount;
    private String userId;
    // getter/setter省略
}

class OrderDTO {
    private String orderId;
    private BigDecimal amount;
    private String userId;
    // getter/setter省略
}

// 测试使用（上层业务统一调用）
public class TestPayment {
    public static void main(String[] args) {
        // 构建订单
        Order order = new Order();
        order.setOrderId("O20260312001");
        order.setAmount(new BigDecimal("99.9"));
        order.setUserId("U1001");

        // 支付宝旧版支付（适配后调用）
        PaymentAdapter alipayOldAdapter = new AlipayOldAdapter(new AlipayOldSDK());
        System.out.println(alipayOldAdapter.pay(order));

        // 支付宝新版支付（适配后调用）
        PaymentAdapter alipayNewAdapter = new AlipayNewAdapter(new AlipayNewSDK());
        System.out.println(alipayNewAdapter.pay(order));

        // 微信支付（适配后调用）
        PaymentAdapter wechatAdapter = new WechatPayAdapter(new WechatPaySDK());
        System.out.println(wechatAdapter.pay(order));
    }
}
```

## 多数据源适配（不同数据库 / 文件格式统一读取）

<font color="#95b3d7">背景</font>：
系统需要读取多种数据源的数据（MySQL、Excel、CSV），但每种数据源的读取接口不同（MySQL 用 JDBC，Excel 用 POI，CSV 用 OpenCSV），上层业务想统一调用`DataReader.readData(String source)`获取数据。

<font color="#95b3d7">代码</font>：
```java
// 1. 统一的目标接口
public interface DataReader {
    // 统一读取数据的方法，返回标准化的List<Map>
    List<Map<String, Object>> readData(String source);
}

// 2. 各数据源的原始接口（第三方/老代码，不能修改）
// MySQL读取工具（JDBC）
public class MySQLDataLoader {
    public List<Map<String, Object>> loadFromMySQL(String jdbcUrl) {
        // 模拟JDBC读取MySQL数据
        List<Map<String, Object>> data = new ArrayList<>();
        Map<String, Object> row = new HashMap<>();
        row.put("id", 1);
        row.put("name", "张三");
        data.add(row);
        return data;
    }
}

// Excel读取工具（POI）
public class ExcelDataLoader {
    public List<List<String>> loadFromExcel(String filePath) {
        // 模拟POI读取Excel数据（原始格式是二维列表）
        List<List<String>> data = new ArrayList<>();
        List<String> header = Arrays.asList("id", "name");
        List<String> row = Arrays.asList("1", "张三");
        data.add(header);
        data.add(row);
        return data;
    }
}

// CSV读取工具（OpenCSV）
public class CSVDataLoader {
    public String[] loadFromCSV(String filePath) {
        // 模拟读取CSV数据（原始格式是字符串数组）
        return new String[]{"id,name", "1,张三"};
    }
}

// 3. 适配器实现
// MySQL适配器
public class MySQLDataAdapter implements DataReader {
    private MySQLDataLoader mySQLDataLoader;

    public MySQLDataAdapter(MySQLDataLoader mySQLDataLoader) {
        this.mySQLDataLoader = mySQLDataLoader;
    }

    @Override
    public List<Map<String, Object>> readData(String jdbcUrl) {
        // MySQL的原始接口返回格式已经符合要求，直接返回
        return mySQLDataLoader.loadFromMySQL(jdbcUrl);
    }
}

// Excel适配器
public class ExcelDataAdapter implements DataReader {
    private ExcelDataLoader excelDataLoader;

    public ExcelDataAdapter(ExcelDataLoader excelDataLoader) {
        this.excelDataLoader = excelDataLoader;
    }

    @Override
    public List<Map<String, Object>> readData(String filePath) {
        // 适配逻辑：将Excel的二维列表转换成List<Map>
        List<List<String>> rawData = excelDataLoader.loadFromExcel(filePath);
        List<Map<String, Object>> result = new ArrayList<>();
        if (rawData.size() < 2) return result;

        // 表头
        List<String> headers = rawData.get(0);
        // 数据行
        for (int i = 1; i < rawData.size(); i++) {
            List<String> row = rawData.get(i);
            Map<String, Object> rowMap = new HashMap<>();
            for (int j = 0; j < headers.size(); j++) {
                rowMap.put(headers.get(j), row.get(j));
            }
            result.add(rowMap);
        }
        return result;
    }
}

// CSV适配器
public class CSVDataAdapter implements DataReader {
    private CSVDataLoader csvDataLoader;

    public CSVDataAdapter(CSVDataLoader csvDataLoader) {
        this.csvDataLoader = csvDataLoader;
    }

    @Override
    public List<Map<String, Object>> readData(String filePath) {
        // 适配逻辑：将CSV的字符串数组转换成List<Map>
        String[] rawData = csvDataLoader.loadFromCSV(filePath);
        List<Map<String, Object>> result = new ArrayList<>();
        if (rawData.length < 2) return result;

        // 表头
        String[] headers = rawData[0].split(",");
        // 数据行
        String[] rowData = rawData[1].split(",");
        Map<String, Object> rowMap = new HashMap<>();
        for (int j = 0; j < headers.length; j++) {
            rowMap.put(headers[j], rowData[j]);
        }
        result.add(rowMap);
        return result;
    }
}

// 测试使用
public class TestDataReader {
    public static void main(String[] args) {
        // 读取MySQL数据
        DataReader mysqlReader = new MySQLDataAdapter(new MySQLDataLoader());
        System.out.println("MySQL数据：" + mysqlReader.readData("jdbc:mysql://localhost:3306/test"));

        // 读取Excel数据
        DataReader excelReader = new ExcelDataAdapter(new ExcelDataLoader());
        System.out.println("Excel数据：" + excelReader.readData("/data/test.xlsx"));

        // 读取CSV数据
        DataReader csvReader = new CSVDataAdapter(new CSVDataLoader());
        System.out.println("CSV数据：" + csvReader.readData("/data/test.csv"));
    }
}
```

## 第三方接口适配（物流查询接口统一）
<font color="#95b3d7">背景</font>：
电商系统需要对接顺丰、圆通、中通的物流查询接口，各接口的请求参数、返回格式都不同：
- 顺丰：`sfQuery(String waybillNo)` → 返回`SFLogisticsDTO`；
- 圆通：`ytQuery(Long mailNo)` → 返回`YTLogisticsVO`；

<font color="#95b3d7">代码</font>：
```java
// 1. 统一的目标接口
public interface LogisticsQuery {
    // 统一查询物流，返回标准化的LogisticsInfo
    LogisticsInfo query(String waybillNo);
}

// 2. 第三方物流接口（不能修改）
// 顺丰接口
public class SFLogisticsSDK {
    public SFLogisticsDTO sfQuery(String waybillNo) {
        SFLogisticsDTO dto = new SFLogisticsDTO();
        dto.setWaybillNo(waybillNo);
        dto.setStatus("已签收");
        dto.setUpdateTime("2026-03-12 10:00:00");
        return dto;
    }
}

// 圆通接口
public class YTLogisticsSDK {
    public YTLogisticsVO ytQuery(Long mailNo) {
        YTLogisticsVO vo = new YTLogisticsVO();
        vo.setMailNo(mailNo.toString());
        vo.setLogisticsStatus(2); // 2代表已签收
        vo.setUpdateTime("2026-03-12 10:00:00");
        return vo;
    }
}

// 3. 标准化的物流信息类
class LogisticsInfo {
    private String waybillNo;
    private String status; // 统一为：待揽收、运输中、已签收
    private String updateTime;
    // getter/setter省略
}

// 第三方DTO/VO
class SFLogisticsDTO {
    private String waybillNo;
    private String status;
    private String updateTime;
    // getter/setter省略
}

class YTLogisticsVO {
    private String mailNo;
    private int logisticsStatus; // 1=运输中，2=已签收
    private String updateTime;
    // getter/setter省略
}

// 4. 适配器实现
// 顺丰适配器
public class SFLogisticsAdapter implements LogisticsQuery {
    private SFLogisticsSDK sfSDK;

    public SFLogisticsAdapter(SFLogisticsSDK sfSDK) {
        this.sfSDK = sfSDK;
    }

    @Override
    public LogisticsInfo query(String waybillNo) {
        // 调用顺丰接口
        SFLogisticsDTO dto = sfSDK.sfQuery(waybillNo);
        // 适配：将SFLogisticsDTO转换成标准化的LogisticsInfo
        LogisticsInfo info = new LogisticsInfo();
        info.setWaybillNo(dto.getWaybillNo());
        info.setStatus(dto.getStatus());
        info.setUpdateTime(dto.getUpdateTime());
        return info;
    }
}

// 圆通适配器
public class YTLogisticsAdapter implements LogisticsQuery {
    private YTLogisticsSDK ytSDK;

    public YTLogisticsAdapter(YTLogisticsSDK ytSDK) {
        this.ytSDK = ytSDK;
    }

    @Override
    public LogisticsInfo query(String waybillNo) {
        // 适配：将字符串运单号转换成圆通需要的Long类型
        Long mailNo = Long.parseLong(waybillNo);
        // 调用圆通接口
        YTLogisticsVO vo = ytSDK.ytQuery(mailNo);
        // 适配：将YTLogisticsVO转换成标准化的LogisticsInfo
        LogisticsInfo info = new LogisticsInfo();
        info.setWaybillNo(vo.getMailNo());
        // 转换状态码为统一描述
        info.setStatus(vo.getLogisticsStatus() == 2 ? "已签收" : "运输中");
        info.setUpdateTime(vo.getUpdateTime());
        return info;
    }
}

// 测试使用
public class TestLogistics {
    public static void main(String[] args) {
        // 查询顺丰物流
        LogisticsQuery sfQuery = new SFLogisticsAdapter(new SFLogisticsSDK());
        System.out.println("顺丰物流：" + sfQuery.query("SF1234567890").getStatus());

        // 查询圆通物流
        LogisticsQuery ytQuery = new YTLogisticsAdapter(new YTLogisticsSDK());
        System.out.println("圆通物流：" + ytQuery.query("YT1234567890").getStatus());
    }
}
```

## 订单状态变更通知

<font color="#95b3d7">背景</font>：
某一订单更新后需要做一系列操作（减库存、通知用户、日志等）

<font color="#95b3d7">代码</font>：
```java
// 1. 定义订单状态变更事件（被观察者的事件载体）
class OrderStatusChangeEvent {
    private String orderId;
    private String oldStatus;
    private String newStatus;

    public OrderStatusChangeEvent(String orderId, String oldStatus, String newStatus) {
        this.orderId = orderId;
        this.oldStatus = oldStatus;
        this.newStatus = newStatus;
    }

    // getter
    public String getOrderId() { return orderId; }
    public String getOldStatus() { return oldStatus; }
    public String getNewStatus() { return newStatus; }
}

// 2. 定义观察者接口
interface OrderStatusListener {
    void onStatusChange(OrderStatusChangeEvent event);
}

// 3. 具体观察者实现
// 短信通知观察者
class SmsNotifyListener implements OrderStatusListener {
    @Override
    public void onStatusChange(OrderStatusChangeEvent event) {
        if ("已支付".equals(event.getNewStatus())) {
            System.out.println("【短信通知】订单" + event.getOrderId() + "已支付，请注意查收包裹");
        } else if ("已取消".equals(event.getNewStatus())) {
            System.out.println("【短信通知】订单" + event.getOrderId() + "已取消，退款将在1-3个工作日到账");
        }
    }
}

// 库存更新观察者
class StockUpdateListener implements OrderStatusListener {
    @Override
    public void onStatusChange(OrderStatusChangeEvent event) {
        if ("已支付".equals(event.getNewStatus())) {
            System.out.println("【库存更新】订单" + event.getOrderId() + "已支付，扣减对应商品库存");
        } else if ("已取消".equals(event.getNewStatus())) {
            System.out.println("【库存更新】订单" + event.getOrderId() + "已取消，恢复对应商品库存");
        }
    }
}

// 日志记录观察者
class OrderLogListener implements OrderStatusListener {
    @Override
    public void onStatusChange(OrderStatusChangeEvent event) {
        System.out.println("【日志记录】订单" + event.getOrderId() + "状态从" + event.getOldStatus() + 
                           "变更为" + event.getNewStatus() + "，时间：" + System.currentTimeMillis());
    }
}

// 4. 被观察者（订单服务）
class OrderService {
    // 存储所有观察者
    private List<OrderStatusListener> listeners = new ArrayList<>();

    // 注册观察者
    public void addListener(OrderStatusListener listener) {
        listeners.add(listener);
    }

    // 移除观察者
    public void removeListener(OrderStatusListener listener) {
        listeners.remove(listener);
    }

    // 订单状态变更（核心业务）
    public void changeOrderStatus(String orderId, String oldStatus, String newStatus) {
        // 1. 执行核心业务逻辑
        System.out.println("【核心业务】订单" + orderId + "状态已更新为" + newStatus);
        
        // 2. 构建事件对象
        OrderStatusChangeEvent event = new OrderStatusChangeEvent(orderId, oldStatus, newStatus);
        
        // 3. 通知所有观察者
        for (OrderStatusListener listener : listeners) {
            listener.onStatusChange(event);
        }
    }
}

// 5. 测试类
public class TestOrderStatus {
    public static void main(String[] args) {
        // 1. 创建被观察者
        OrderService orderService = new OrderService();
        
        // 2. 注册观察者
        orderService.addListener(new SmsNotifyListener());
        orderService.addListener(new StockUpdateListener());
        orderService.addListener(new OrderLogListener());
        
        // 3. 触发订单状态变更
        System.out.println("===== 测试1：订单支付 =====");
        orderService.changeOrderStatus("O20260312001", "待支付", "已支付");
        
        System.out.println("\n===== 测试2：订单取消 =====");
        orderService.changeOrderStatus("O20260312001", "已支付", "已取消");
    }
}
```

## 用户注册后自动执行多任务

<font color="#95b3d7">背景</font>：


<font color="#95b3d7">代码</font>：
```java
// 1. 定义用户注册事件
class UserRegisterEvent {
    private String userId;
    private String phone;
    private String email;

    public UserRegisterEvent(String userId, String phone, String email) {
        this.userId = userId;
        this.phone = phone;
        this.email = email;
    }

    // getter
    public String getUserId() { return userId; }
    public String getPhone() { return phone; }
    public String getEmail() { return email; }
}

// 2. 定义观察者接口
interface UserRegisterListener {
    void onRegister(UserRegisterEvent event);
}

// 3. 具体观察者实现
// 短信通知观察者
class UserSmsListener implements UserRegisterListener {
    @Override
    public void onRegister(UserRegisterEvent event) {
        System.out.println("【注册短信】欢迎用户" + event.getUserId() + "注册，手机号：" + 
                           event.getPhone() + "，验证码已发送");
    }
}

// 积分初始化观察者
class UserPointListener implements UserRegisterListener {
    @Override
    public void onRegister(UserRegisterEvent event) {
        System.out.println("【积分初始化】用户" + event.getUserId() + "注册成功，初始化100积分");
    }
}

// 邮件通知观察者
class UserEmailListener implements UserRegisterListener {
    @Override
    public void onRegister(UserRegisterEvent event) {
        System.out.println("【注册邮件】已向" + event.getEmail() + "发送欢迎邮件，请注意查收");
    }
}

// 4. 被观察者（用户服务）
class UserService {
    private List<UserRegisterListener> listeners = new ArrayList<>();

    // 注册观察者
    public void addListener(UserRegisterListener listener) {
        listeners.add(listener);
    }

    // 用户注册核心方法
    public void register(String userId, String phone, String email) {
        // 1. 核心业务：保存用户
        System.out.println("【核心业务】用户" + userId + "注册成功，保存用户信息到数据库");
        
        // 2. 构建事件
        UserRegisterEvent event = new UserRegisterEvent(userId, phone, email);
        
        // 3. 通知所有观察者
        for (UserRegisterListener listener : listeners) {
            listener.onRegister(event);
        }
    }
}

// 5. 测试类
public class TestUserRegister {
    public static void main(String[] args) {
        UserService userService = new UserService();
        // 注册观察者
        userService.addListener(new UserSmsListener());
        userService.addListener(new UserPointListener());
        userService.addListener(new UserEmailListener());
        
        // 触发注册
        System.out.println("===== 测试：用户注册 =====");
        userService.register("U1001", "13800138000", "test@example.com");
    }
}
```
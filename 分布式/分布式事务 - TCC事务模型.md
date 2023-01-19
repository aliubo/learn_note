## 简介

如果服务A和服务B之间是同步调用，比如服务C需要按流程调服务A和服务B，服务A和服务B要么一起成功，要么一起失败。  
针对这种情况，目前业内普遍推荐使用TCC事务来解决的  
TCC的全称是（Try-Confirm-Cancel）  

## 业务场景样例

支付服务 需要完成以下调用 订单服务（修改订单状态）、账户服务（扣除余额）、库存服务（扣减库存数量）  
为了达到事务的效果，要么一起成功，要么一起失败  

为了达到这种效果，每个服务提供三种接口
```java
// 以订单服务为例
orderClient.tryUpateStatus();       // T - try
orderClient.confirmUpateStatus();   // C - confirm
orderClient.cancelUpateStatus();    // C - cancel
```

TCC的缺点主要在于对于代码侵入性大，每套业务逻辑都要这么拆分成三个接口。

伪代码如下

```java
public class PayServiceImpl{
    private OrderClient orderClient;
    private AccountClient accountClient;
    private RepositoryClient repositoryClient;
    public void makePayment throws Throwable{
        try{
            orderClient.tryUpdateStatus();  // 修改订单状态
            accountClient.tryDecrease();    // 扣款
            repositoryClient.tryDesrease(); // 库存减少
        }catch(Throwable t){
            // 遇到错误回滚事务
            orderClient.cancelUpdateStatus();
            accountClient.cancelDecrease();
            repositoryClient.cancelDecrease();
        }
        // 提交事务
        orderClient.confirmUpdateStatus();
        accountClient.confirmDecrease();
        repositoryClient.confirmDecrease();
    }
}
```

这里用了一段简单的代码来描述这个过程，但是这段代码存在很多问题，比如cancel和confirm出现异常如何处理？还有涉及到大量逻辑重复问题。

## hmily框架

分布式事务框架

## Seata框架

参见`分布式事务 - Seata框架.md`

## 参考链接

https://cloud.tencent.com/developer/article/1844341
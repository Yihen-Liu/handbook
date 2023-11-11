#### RPC

1. 测试RPC

    ```
    BSC网络名称
    HK-jppoc
    新的 RPC URL
    http://164.52.93.87:8545/
    链 ID
    820666
    货币符号
    Hkjp
    区块浏览器 URL
    （可选）
    ```

1. 日本环境 RPC

    ```
    18.178.0.240:8545
    ```
    
1. 

#### Mysql

1. 测试网

    ```
    mysql DB:
    [database]
    User = root
    Password = 8lab
    Host = 10.182.1.77:3306
    # bsc数据库名
    Bsc = shardinghk
    
    P.S: 经常连不上
    ```
    
    ```
    210.73.218.171
    rsa内容：
    -----BEGIN RSA PRIVATE KEY-----
    MIIEpQIBAAKCAQEA23BAvaWpWNDAoF5eb1O9zRMeUCIbDYke9lQ8WCKIEnXW0Gew
    Q66l7JYwD7hiodyaFMyFe0W4i7eAbXES64V7bkJFwNDYXdgwj4IP/IkBZ52zypfb
    QreNjCVxy0WiURZZt7ipfrbpDv+FvY7TwRXu3dRcGcG3IYysT6f5ENEzw/m84YWD
    7ptOCtDMNAo5XEanPQU/R6AVBnUem/hywi9MkzLTv3UKsiIfGIBvG+8YgDyEmxst
    ZDTE8y2XlDXqgD3Nf4oS9HPZk6qzO9cWrDb2xfaIYB8Rc4CI/FLLFUdTn50GqUBY
    BLsSd/vxQj5mMGoi8Xd4IAexNVsQSqvRhbgUjwIDAQABAoIBAQCu91c3n8JihbhB
    Zl1HyO6aeHcAD+GgLkgYwtuGrqnuhjTs4PAjVzsHZE0YC73hL4NPuC9qNhJKnNry
    6GjckAb1yDPT5PHQCdPWaS8T/a24D39OtzxlevOK3kRYfsJIg1iv67aByZgUlFrv
    5NUkrLdT+sIg61t4jbDKprUp2pS62Yhu/P/4FgzmrPaHWuoQre6Zg5dWvE+pBcmp
    YheK72/m9hXRS4GZRx29IJMshFNOZL1M/ey+jbU/9sedj+pV42hr3T6e8FZf95Xq
    eVtXAM9KfPGFhE1yUJ0cIC4xuwgueUdgrx08iUqos3bCoaNVcX5kVU05z0yXuTSL
    ii2fjkA5AoGBAPmYVhAhTKx966o68O8Y8PD1ISerKowbxd+NgJhoDXlEDRfei9QM
    TYV+IB06jYKRV6VNeGPVPtC1u3RtPEgMoQVzUrrp7H118HiVik2noNvhsJFH+Nea
    oXHj45ll+eub+wYtvBYx5HJvIpkPVSAkLSnWv5b7ueu7iONiPf3tpMajAoGBAOER
    zyqk3YlXMTqLjcXWtokZfboswe3AlvaYAqI39hooRgKLp/VnO1VD0/roNUFIqL4o
    V9uM4Z+7o/Fx3UZDH3PNYfBVCeS/zFElUPwQdL210wEFv9S/TZERhTa4sBaebQn4
    3cSiiTla+KHsm50v1eXWVXqv9+OXGUYorTHqtBUlAoGBALFk7w4pzKfwGzXzDFiz
    PlPTtUvPYL8R4jIADTzE/4aHslKbrn/4eoR9Xu/HNNpu2H85L26tGicWcvPNy4Fd
    0HfiPhNwvM9yqoXZquGEWVTN9ENdhuQeF86tbI8TJmypgOEkUkDoFviqOknU1uiw
    LZVF9welQ7/imukZYvv+EhXHAoGBAMhTba1rKLQBo5OUew/IWJgW1E1NYR8Y+EVs
    b4ure6U0i3vgihJnW+w8fwUogZ4l6eu3RNvpvTjLbtSMoILVY71S5QVg63lrLZRc
    PoTcsMvadoDGeUQHMicZDRTzteesAymJFPrcIH+odPzK+Icj+KKl71dQILe12Y0U
    z3NKkBbxAoGALzauf8OLySz8wQKMpGYox8acVn9NANFOrkXfR2OM7+2VmvupeUVp
    t1ljDghIlVKH290qWWRNXq/K1WsdiV/BbLHFhBcSBU/HyNESlYjrizKxQImblhae
    KBoqiCTqkkCNq0c6ymrgjclCzENEtPVDV6BGIUCwHeAjyKNFuRc7Hkc=
    -----END RSA PRIVATE KEY-----
    ```
    
    

#### Postgress

1. 测试网

    ```
    Host:192.168.1.99 
    port: 5432
    User:octa8lab
    Password: octa8lab
    ==============================
    User = octa8lab
    Password = octa8lab
    Host = 101.251.205.210:45432
    ==============================
    Host: 106.3.133.180
    User:postgres
    Password:octa8lab
    ```
    
1. 线上环境

    ```
    ==============Japan===============
    Host： postgres-explorer-service-svc
    Port： 45432
    DB：shardingjp1
    User：test
    Password：test
    
    
    ```
    
    

#### SSH机器

1. 测试公网

    ```
    ssh root@10.182.1.77 -p 22
    公钥登录
    使用octa_win_freedom WIFI网关
    ```

2. 测试内网(北京环境)

    ```
    192.168.1.223
    192.168.1.224
    192.168.1.225
    
    User: root
    Password: Trust714_Test@2111
    ```

3. explorer联调机器(香港环境)

    ```
    host:  106.3.133.179
    user:  dev-user
    password: _8LaBP@s$w0rd
    
    host:  106.3.133.180
    user:  dev-user
    password:_8LaBP@s$w0rd
    ```
    
    

#### WIFI

```
octa_win_freedom 8L@BExP0!!!!

octa_security    8L@BexCe
```



#### Redis

```
180 redis连接信息
Host: 106.3.133.180
Port: 6379
Password： 8lab.org@Helloworld
```



#### 禅道

```
UserName: liuyh
Password: 11111111
```



#### Elastic Service

```
Dashboard: http://106.3.133.180:9800/

Connect输入框填： http://elastic:elastic@192.168.1.69:9200 回车可搜索explorer目前在用的服务集群；
```



#### Tendermint测试环境

```
TM-RPC http://106.3.133.180:46657
```


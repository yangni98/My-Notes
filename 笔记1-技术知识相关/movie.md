### 结果封装

前后端统一结果

因为是前后端分离的项目，所以我们有必要统一一个结果返回封装类，这样前后端交互的时候有个统一的标准，约定结果返回的数据是正常的或者遇到异常了。

这里我们用到了一个Result的类，这个用于我们的异步统一返回的结果封装。一般来说，结果里面有几个要素必要的

- 是否成功，可用code表示（如200表示成功，400表示异常）
- 结果消息
- 结果数据

所以可得到封装如下：

- com.markerhub.common.lang.Result

```
@Data
public class Result implements Serializable {
    private int code; // 200是正常，非200表示异常
    private String msg;
    private Object data;

    public static Result succ(Object data) {
        return succ(200, "操作成功", data);
    }
    public static Result succ(int code, String msg, Object data) {
        Result r = new Result();
        r.setCode(code);
        r.setMsg(msg);
        r.setData(data);
        return r;
    }
    public static Result fail(String msg) {
        return fail(400, msg, null);
    }
    public static Result fail(String msg, Object data) {
        return fail(400, msg, data);
    }
    public static Result fail(int code, String msg, Object data) {
        Result r = new Result();
        r.setCode(code);
        r.setMsg(msg);
        r.setData(data);
        return r;
    }
}
```

另外出了在结果封装类上的code可以提现数据是否正常，我们还可以通过http的状态码来提现访问是否遇到了异常，比如401表示五权限拒绝访问等，注意灵活使用。











引入securety







引入redis

并且重写redis工具类


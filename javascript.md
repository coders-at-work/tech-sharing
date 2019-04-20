1. 类型
    1. 分类
        - 语言类型 7 种： Undefined, Null, String, Number, Boolean, Symbol, Object
            - 基本类型(Primitive): 前 6 种
            - 对象类型： Object
            - **注意： javascript 语言不存在其它类型**
        - 内部实现相关类型
    2. 类型和值
    
    语言类型 | 语言规定的值 | 程序开发的字面量
    ------- | ---------- | -------------
    undifined | undefined | 1. undefined, 不是语言的关键字，而是 global object 的一个 property。在 ES5 之前可以被改写，ES5 开始变为只读。但仍然可以声明局部变量(如函数内部）名为 undefined. 2. void 操作符把其后的参数转换为 undefined. (void 0) => undefined
    3. 类型转换

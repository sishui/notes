## c++ 11 特性总结

  * __cplusplus宏

    在c++ 03中的值是199711L,在c++11中大于这个值
  
  * constexpr
    编译器检测是否常量表达式
```
      constexpr int MAX_LINE = 10; // 常量表达式，必须初始化
      constexpr int sz = func();   // 只有当func是一个constexpr函数的时才是
```   

  * 对齐方式
    * `alignas`
    * `alignof`
```
       alignas(int) char s1[32]; // 以int大小对齐
       alignas(16) char s2[32];  // 以16字节对齐     
       constexpr int sz = alignof(int); // 返回 int 的对齐方式
```
  * attribute
```
    void func [[noreturn]](){ //永不返回
    }
```
  
  * 自动类型推导
    * `auto`    
    * `decltype`
```
       auto x = 123; // 相当于 int x = 123;
       decltype(x);  // 
       
       templete<class T>
       decltype(x) add(T x， T y){	//error 返回值访问不了 x,y
           return x+y;
       }
       
       auto add(T x， T y) -> decltype(x+y) {	//ok
           return x+y;
       } 
```
  
  * 新的`enum`(当然兼容之前的版本)
```
    euum Color03 {r, g, b}
    enum class Color11 {r, g, b};
    int r = Color03::r; //ok
    int r = Color11::r; //error 禁止
    enum class Color : char {r, g, b}; //表示一个字节
```
  
  * 默认/禁用函数(可作用于 构造,拷贝构造，赋值，析构)
    * `defaut`;
    * `delete`;
```
      class Clazz{
      public:
          Clazz(int x) = default; //默认构造函数是这个
          Clazz& operator=(const Clazz& c) = delete; //禁用赋值函数
          Clazz(const Clazz&) = delete; //禁用拷贝构造
      };
```
  
  * 抛出异常限制
    * `noexcept`
```
      void func() noexcept { } // func 函数永远不会抛出异常
      
      void func(T& t) noexcept(noexcept(t.test())) //t.test() 如果有异常可以抛出
``` 
  * for循环
    ```
      std::vertor<int> v;
      ... //假设此处对 v 进行了赋值
      for( auto x: v){
          std::cout << x << std::endl;
      }
    ```
  
  * 成员变量的初始值
```
      class Clazz{
      public:
         Clazz(){} // 被调用时x,y 会分别被初始化为 100、200;
         Clazz(int m, int n) : x(m), y(n) {} //被调用时，会被初始化为参数m 和 n 的值
      private:
          int x = 100;
          int y = 200;
      };
```  
  * 构造函数可被继承
```
      class Base{
      public:
          Base(int);
      };
      class Clazz : Base{
      public:
          using Base::Base; //隐式声明了Base(int)
          int x = 321;
      };
      
      int  main(){
          Clazz clz(123); //!!!但clz.x的值是，321 （！！！这里貌似有点扯淡了）;
      }
``` 
      
  * `inline namespace`
```
      inline namespace V2{	//inline声明
          void func();
      }
      
      namespace V1{
          void func();
      }
      
      namespace MY{
      #include "v1.h"
      #include "v2.h"
      }
      
      //
      using namespace MY;
      V2::func(); //V2里的
      V1::func(); //V1里的
      func(); //默认调用V2里的
```     
  
  * Lambda 表达式
    * [] 不捕捉变量
    * [&] 引用方式捕捉
    * [=] 复制方式捕捉
    * [=,&var] 变量var通过引用捕捉，其余通过复制方式捕捉
    * [var] 只捕捉变量var(复制方式）
    * [this] 捕捉this指针 
```
       class Clazz{
       public:
           int a = 1000;
           Clazz(){}
           void func1(){
               int z = 100;
               auto f = [=](int x, int y){
                 return x+y+z;
               };
               int result = f(1, 2); //103;
           }
           
           void func2(){
               int z = 100;
               auto f = [&](int x, int y){
                 z = 0;
                 return x+y+z;
               };
               int result = f(1, 2); //3,且 z 被改变;
           }
           
           void func3(){
               [this] (){
                   std::cout<<this->a<<std::endl; //ok
               }
           }
       }
```

  * override/final
```
       class Base{
           void test() final; //不能被子类重写
           void func(int);
       }
       class Clazz: Base{
           void test(); //error 不能被重新，父类是final;
           void func(int) override; //显示重写
       }
```
  
  * 原生字符串标识
    * R”(…)”
    
  * `static_assert`
    * 编译阶段检查
    ```
    static_assert(sizeof(int)>4, "error.."); //ok
    static_assert(p == NULL, "error.."); //不行，因为p 不只常量
    ```  

  * test
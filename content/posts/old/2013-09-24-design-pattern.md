---
title: 设计模式理解
author: fatkun
type: post
date: 2013-09-24T15:55:14+00:00
url: /2013/09/design-pattern.html
duoshuo_thread_id:
  - 6300410041086247682
wp-syntax-cache-content:
  - |
    a:9:{i:1;s:7798:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;">抽象工厂模式（python）
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">class</span> IUser:
        <span style="color: #ff7700;font-weight:bold;">def</span> GetUser<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>:
            <span style="color: #ff7700;font-weight:bold;">pass</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">class</span> IDepartment:
        <span style="color: #ff7700;font-weight:bold;">def</span> GetDepartment<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>:
            <span style="color: #ff7700;font-weight:bold;">pass</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">class</span> CAccessUser<span style="color: black;">&#40;</span>IUser<span style="color: black;">&#41;</span>:
        <span style="color: #ff7700;font-weight:bold;">def</span> GetUser<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>:
            <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">&quot;Access GetUser&quot;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">class</span> CAccessDepartment<span style="color: black;">&#40;</span>IDepartment<span style="color: black;">&#41;</span>:
        <span style="color: #ff7700;font-weight:bold;">def</span> GetDepartment<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>:
            <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">&quot;Access GetDepartment&quot;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">class</span> CSqlUser<span style="color: black;">&#40;</span>IUser<span style="color: black;">&#41;</span>:
        <span style="color: #ff7700;font-weight:bold;">def</span> GetUser<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>:
            <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">&quot;Sql GetUser&quot;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">class</span> CSqlDepartment<span style="color: black;">&#40;</span>IDepartment<span style="color: black;">&#41;</span>:
        <span style="color: #ff7700;font-weight:bold;">def</span> GetDepartment<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>:
            <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">&quot;Sql GetDepartment&quot;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">class</span> IFactory:
        <span style="color: #ff7700;font-weight:bold;">def</span> CreateUser<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>:
            <span style="color: #ff7700;font-weight:bold;">pass</span>
        <span style="color: #ff7700;font-weight:bold;">def</span> CreateDepartment<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>:
            <span style="color: #ff7700;font-weight:bold;">pass</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">class</span> AccessFactory<span style="color: black;">&#40;</span>IFactory<span style="color: black;">&#41;</span>:
        <span style="color: #ff7700;font-weight:bold;">def</span> CreateUser<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>:
            temp<span style="color: #66cc66;">=</span>CAccessUser<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
            <span style="color: #ff7700;font-weight:bold;">return</span> temp
        <span style="color: #ff7700;font-weight:bold;">def</span> CreateDepartment<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>:
            temp <span style="color: #66cc66;">=</span> CAccessDepartment<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
            <span style="color: #ff7700;font-weight:bold;">return</span> temp
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">class</span> SqlFactory<span style="color: black;">&#40;</span>IFactory<span style="color: black;">&#41;</span>:
        <span style="color: #ff7700;font-weight:bold;">def</span> CreateUser<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>:
            temp <span style="color: #66cc66;">=</span> CSqlUser<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
            <span style="color: #ff7700;font-weight:bold;">return</span> temp
        <span style="color: #ff7700;font-weight:bold;">def</span> CreateDepartment<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>:
            temp <span style="color: #66cc66;">=</span> CSqlDepartment<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
            <span style="color: #ff7700;font-weight:bold;">return</span> temp
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> __name__ <span style="color: #66cc66;">==</span> <span style="color: #483d8b;">&quot;__main__&quot;</span>:
        factory <span style="color: #66cc66;">=</span> SqlFactory<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
        <span style="color: #dc143c;">user</span><span style="color: #66cc66;">=</span>factory.<span style="color: black;">CreateUser</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
        depart<span style="color: #66cc66;">=</span>factory.<span style="color: black;">CreateDepartment</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
        <span style="color: #dc143c;">user</span>.<span style="color: black;">GetUser</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
        depart.<span style="color: black;">GetDepartment</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">抽象工厂模式（python）
    
    class IUser:
        def GetUser(self):
            pass
    
    class IDepartment:
        def GetDepartment(self):
            pass
    
    class CAccessUser(IUser):
        def GetUser(self):
            print &quot;Access GetUser&quot;
    
    class CAccessDepartment(IDepartment):
        def GetDepartment(self):
            print &quot;Access GetDepartment&quot;
    
    class CSqlUser(IUser):
        def GetUser(self):
            print &quot;Sql GetUser&quot;
    
    class CSqlDepartment(IDepartment):
        def GetDepartment(self):
            print &quot;Sql GetDepartment&quot;
    
    class IFactory:
        def CreateUser(self):
            pass
        def CreateDepartment(self):
            pass
    
    class AccessFactory(IFactory):
        def CreateUser(self):
            temp=CAccessUser()
            return temp
        def CreateDepartment(self):
            temp = CAccessDepartment()
            return temp
    
    class SqlFactory(IFactory):
        def CreateUser(self):
            temp = CSqlUser()
            return temp
        def CreateDepartment(self):
            temp = CSqlDepartment()
            return temp
    
    if __name__ == &quot;__main__&quot;:
        factory = SqlFactory()
        user=factory.CreateUser()
        depart=factory.CreateDepartment()
        user.GetUser()
        depart.GetDepartment()</p></div>
    ";i:2;s:3041:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> ImageReaderFactory <span style="color: #009900;">&#123;</span>
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> ImageReader imageReaderFactoryMethod<span style="color: #009900;">&#40;</span><span style="color: #003399;">InputStream</span> is<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            ImageReader product <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #339933;">;</span>
    &nbsp;
            <span style="color: #000066; font-weight: bold;">int</span> imageType <span style="color: #339933;">=</span> determineImageType<span style="color: #009900;">&#40;</span>is<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #000000; font-weight: bold;">switch</span> <span style="color: #009900;">&#40;</span>imageType<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                <span style="color: #000000; font-weight: bold;">case</span> ImageReaderFactory.<span style="color: #006633;">GIF</span><span style="color: #339933;">:</span>
                    product <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> GifReader<span style="color: #009900;">&#40;</span>is<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #000000; font-weight: bold;">case</span> ImageReaderFactory.<span style="color: #006633;">JPEG</span><span style="color: #339933;">:</span>
                    product <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> JpegReader<span style="color: #009900;">&#40;</span>is<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #666666; font-style: italic;">//...</span>
            <span style="color: #009900;">&#125;</span>
            <span style="color: #000000; font-weight: bold;">return</span> product<span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">public class ImageReaderFactory {
        public static ImageReader imageReaderFactoryMethod(InputStream is) {
            ImageReader product = null;
    
            int imageType = determineImageType(is);
            switch (imageType) {
                case ImageReaderFactory.GIF:
                    product = new GifReader(is);
                case ImageReaderFactory.JPEG:
                    product = new JpegReader(is);
                //...
            }
            return product;
        }
    }</p></div>
    ";i:3;s:16240:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"> <span style="color: #008000; font-style: italic; font-weight: bold;">/** &quot;Product&quot; */</span>
     <span style="color: #000000; font-weight: bold;">class</span> Pizza <span style="color: #009900;">&#123;</span>
       <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #003399;">String</span> dough <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;&quot;</span><span style="color: #339933;">;</span>
       <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #003399;">String</span> sauce <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;&quot;</span><span style="color: #339933;">;</span>
       <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #003399;">String</span> topping <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;&quot;</span><span style="color: #339933;">;</span>
    &nbsp;
       <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> setDough <span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> dough<span style="color: #009900;">&#41;</span>     <span style="color: #009900;">&#123;</span> <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">dough</span> <span style="color: #339933;">=</span> dough<span style="color: #339933;">;</span> <span style="color: #009900;">&#125;</span>
       <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> setSauce <span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> sauce<span style="color: #009900;">&#41;</span>     <span style="color: #009900;">&#123;</span> <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">sauce</span> <span style="color: #339933;">=</span> sauce<span style="color: #339933;">;</span> <span style="color: #009900;">&#125;</span>
       <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> setTopping <span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> topping<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span> <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">topping</span> <span style="color: #339933;">=</span> topping<span style="color: #339933;">;</span> <span style="color: #009900;">&#125;</span>
     <span style="color: #009900;">&#125;</span>
    &nbsp;
     <span style="color: #0000ff;">''</span><span style="color: #008000; font-style: italic; font-weight: bold;">/** &quot;Abstract Builder&quot; */</span><span style="color: #0000ff;">''</span>
     <span style="color: #000000; font-weight: bold;">abstract</span> <span style="color: #000000; font-weight: bold;">class</span> PizzaBuilder <span style="color: #009900;">&#123;</span>
       <span style="color: #000000; font-weight: bold;">protected</span> Pizza pizza<span style="color: #339933;">;</span>
    &nbsp;
       <span style="color: #000000; font-weight: bold;">public</span> Pizza getPizza<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span> <span style="color: #000000; font-weight: bold;">return</span> pizza<span style="color: #339933;">;</span> <span style="color: #009900;">&#125;</span>
       <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> createNewPizzaProduct<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span> pizza <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Pizza<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #009900;">&#125;</span>
    &nbsp;
       <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">abstract</span> <span style="color: #000066; font-weight: bold;">void</span> buildDough<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
       <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">abstract</span> <span style="color: #000066; font-weight: bold;">void</span> buildSauce<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
       <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">abstract</span> <span style="color: #000066; font-weight: bold;">void</span> buildTopping<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
     <span style="color: #009900;">&#125;</span>
    &nbsp;
     <span style="color: #008000; font-style: italic; font-weight: bold;">/** &quot;ConcreteBuilder&quot; */</span>
     <span style="color: #000000; font-weight: bold;">class</span> HawaiianPizzaBuilder <span style="color: #000000; font-weight: bold;">extends</span> PizzaBuilder <span style="color: #009900;">&#123;</span>
       <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> buildDough<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>   <span style="color: #009900;">&#123;</span> pizza.<span style="color: #006633;">setDough</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;cross&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #009900;">&#125;</span>
       <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> buildSauce<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>   <span style="color: #009900;">&#123;</span> pizza.<span style="color: #006633;">setSauce</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;mild&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #009900;">&#125;</span>
       <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> buildTopping<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span> pizza.<span style="color: #006633;">setTopping</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;ham+pineapple&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #009900;">&#125;</span>
     <span style="color: #009900;">&#125;</span>
    &nbsp;
     <span style="color: #008000; font-style: italic; font-weight: bold;">/** &quot;ConcreteBuilder&quot; */</span>
     <span style="color: #000000; font-weight: bold;">class</span> SpicyPizzaBuilder <span style="color: #000000; font-weight: bold;">extends</span> PizzaBuilder <span style="color: #009900;">&#123;</span>
       <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> buildDough<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>   <span style="color: #009900;">&#123;</span> pizza.<span style="color: #006633;">setDough</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;pan baked&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #009900;">&#125;</span>
       <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> buildSauce<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>   <span style="color: #009900;">&#123;</span> pizza.<span style="color: #006633;">setSauce</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;hot&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #009900;">&#125;</span>
       <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> buildTopping<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span> pizza.<span style="color: #006633;">setTopping</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;pepperoni+salami&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #009900;">&#125;</span>
     <span style="color: #009900;">&#125;</span>
    &nbsp;
     <span style="color: #0000ff;">''</span><span style="color: #008000; font-style: italic; font-weight: bold;">/** &quot;Director&quot; */</span><span style="color: #0000ff;">''</span>
     <span style="color: #000000; font-weight: bold;">class</span> Waiter <span style="color: #009900;">&#123;</span>
       <span style="color: #000000; font-weight: bold;">private</span> PizzaBuilder pizzaBuilder<span style="color: #339933;">;</span>
    &nbsp;
       <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> setPizzaBuilder <span style="color: #009900;">&#40;</span>PizzaBuilder pb<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span> pizzaBuilder <span style="color: #339933;">=</span> pb<span style="color: #339933;">;</span> <span style="color: #009900;">&#125;</span>
       <span style="color: #000000; font-weight: bold;">public</span> Pizza getPizza<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span> <span style="color: #000000; font-weight: bold;">return</span> pizzaBuilder.<span style="color: #006633;">getPizza</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #009900;">&#125;</span>
    &nbsp;
       <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> constructPizza<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
         pizzaBuilder.<span style="color: #006633;">createNewPizzaProduct</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
         pizzaBuilder.<span style="color: #006633;">buildDough</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
         pizzaBuilder.<span style="color: #006633;">buildSauce</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
         pizzaBuilder.<span style="color: #006633;">buildTopping</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
       <span style="color: #009900;">&#125;</span>
     <span style="color: #009900;">&#125;</span>
    &nbsp;
     <span style="color: #008000; font-style: italic; font-weight: bold;">/** A customer ordering a pizza. */</span>
     <span style="color: #000000; font-weight: bold;">class</span> BuilderExample <span style="color: #009900;">&#123;</span>
       <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">void</span> main<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> args<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
         Waiter waiter <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Waiter<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
         PizzaBuilder hawaiian_pizzabuilder <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> HawaiianPizzaBuilder<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
         PizzaBuilder spicy_pizzabuilder <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> SpicyPizzaBuilder<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
         waiter.<span style="color: #006633;">setPizzaBuilder</span> <span style="color: #009900;">&#40;</span> hawaiian_pizzabuilder <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
         waiter.<span style="color: #006633;">constructPizza</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
         Pizza pizza <span style="color: #339933;">=</span> waiter.<span style="color: #006633;">getPizza</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
       <span style="color: #009900;">&#125;</span>
     <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;"> /** &quot;Product&quot; */
     class Pizza {
       private String dough = &quot;&quot;;
       private String sauce = &quot;&quot;;
       private String topping = &quot;&quot;;
    
       public void setDough (String dough)     { this.dough = dough; }
       public void setSauce (String sauce)     { this.sauce = sauce; }
       public void setTopping (String topping) { this.topping = topping; }
     }
    
     ''/** &quot;Abstract Builder&quot; */''
     abstract class PizzaBuilder {
       protected Pizza pizza;
    
       public Pizza getPizza() { return pizza; }
       public void createNewPizzaProduct() { pizza = new Pizza(); }
    
       public abstract void buildDough();
       public abstract void buildSauce();
       public abstract void buildTopping();
     }
    
     /** &quot;ConcreteBuilder&quot; */
     class HawaiianPizzaBuilder extends PizzaBuilder {
       public void buildDough()   { pizza.setDough(&quot;cross&quot;); }
       public void buildSauce()   { pizza.setSauce(&quot;mild&quot;); }
       public void buildTopping() { pizza.setTopping(&quot;ham+pineapple&quot;); }
     }
    
     /** &quot;ConcreteBuilder&quot; */
     class SpicyPizzaBuilder extends PizzaBuilder {
       public void buildDough()   { pizza.setDough(&quot;pan baked&quot;); }
       public void buildSauce()   { pizza.setSauce(&quot;hot&quot;); }
       public void buildTopping() { pizza.setTopping(&quot;pepperoni+salami&quot;); }
     }
    
     ''/** &quot;Director&quot; */''
     class Waiter {
       private PizzaBuilder pizzaBuilder;
    
       public void setPizzaBuilder (PizzaBuilder pb) { pizzaBuilder = pb; }
       public Pizza getPizza() { return pizzaBuilder.getPizza(); }
    
       public void constructPizza() {
         pizzaBuilder.createNewPizzaProduct();
         pizzaBuilder.buildDough();
         pizzaBuilder.buildSauce();
         pizzaBuilder.buildTopping();
       }
     }
    
     /** A customer ordering a pizza. */
     class BuilderExample {
       public static void main(String[] args) {
         Waiter waiter = new Waiter();
         PizzaBuilder hawaiian_pizzabuilder = new HawaiianPizzaBuilder();
         PizzaBuilder spicy_pizzabuilder = new SpicyPizzaBuilder();
    
         waiter.setPizzaBuilder ( hawaiian_pizzabuilder );
         waiter.constructPizza();
    
         Pizza pizza = waiter.getPizza();
       }
     }</p></div>
    ";i:4;s:4710:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.util.*</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> Fruit
    <span style="color: #009900;">&#123;</span>
        <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000000; font-weight: bold;">final</span> Map<span style="color: #339933;">&lt;</span><span style="color: #003399;">String</span>,Fruit<span style="color: #339933;">&gt;</span> types <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> HashMap<span style="color: #339933;">&lt;</span><span style="color: #003399;">String</span>,Fruit<span style="color: #339933;">&gt;</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000000; font-weight: bold;">final</span> <span style="color: #003399;">String</span> type<span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #666666; font-style: italic;">// using a private constructor to force use of the factory method.</span>
        <span style="color: #000000; font-weight: bold;">private</span> Fruit<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> type<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">type</span> <span style="color: #339933;">=</span> type<span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #008000; font-style: italic; font-weight: bold;">/**
         * Lazy Factory method, gets the Fruit instance associated with a
         * certain type. Instantiates new ones as needed.
         * @param type Any string that describes a fruit type, e.g. &quot;apple&quot;
         * @return The Fruit instance associated with that type.
         */</span>
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000000; font-weight: bold;">synchronized</span> Fruit getFruit<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> type<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #000000; font-weight: bold;">if</span><span style="color: #009900;">&#40;</span><span style="color: #339933;">!</span>types.<span style="color: #006633;">containsKey</span><span style="color: #009900;">&#40;</span>type<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span>
            types.<span style="color: #006633;">put</span><span style="color: #009900;">&#40;</span>type, <span style="color: #000000; font-weight: bold;">new</span> Fruit<span style="color: #009900;">&#40;</span>type<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// Lazy initialization</span>
          <span style="color: #000000; font-weight: bold;">return</span> types.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span>type<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">import java.util.*;
    
    public class Fruit
    {
        private static final Map&lt;String,Fruit&gt; types = new HashMap&lt;String,Fruit&gt;();
        private final String type;
    
        // using a private constructor to force use of the factory method.
        private Fruit(String type) {
          this.type = type;
        }
    
        /**
         * Lazy Factory method, gets the Fruit instance associated with a
         * certain type. Instantiates new ones as needed.
         * @param type Any string that describes a fruit type, e.g. &quot;apple&quot;
         * @return The Fruit instance associated with that type.
         */
        public static synchronized Fruit getFruit(String type) {
          if(!types.containsKey(type))
            types.put(type, new Fruit(type)); // Lazy initialization
          return types.get(type);
        }
    }</p></div>
    ";i:5;s:8140:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #008000; font-style: italic; font-weight: bold;">/** Prototype Class **/</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> Cookie <span style="color: #000000; font-weight: bold;">implements</span> <span style="color: #003399;">Cloneable</span> <span style="color: #009900;">&#123;</span>
    &nbsp;
       <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #003399;">Object</span> clone<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>
       <span style="color: #009900;">&#123;</span>
           <span style="color: #000000; font-weight: bold;">try</span><span style="color: #009900;">&#123;</span>
               <span style="color: #666666; font-style: italic;">//In an actual implementation of this pattern you would now attach references to</span>
               <span style="color: #666666; font-style: italic;">//the expensive to produce parts from the copies that are held inside the prototype.</span>
               <span style="color: #000000; font-weight: bold;">return</span> <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">getClass</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">newInstance</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
           <span style="color: #009900;">&#125;</span>
           <span style="color: #000000; font-weight: bold;">catch</span><span style="color: #009900;">&#40;</span><span style="color: #003399;">InstantiationException</span> e<span style="color: #009900;">&#41;</span>
           <span style="color: #009900;">&#123;</span>
              e.<span style="color: #006633;">printStackTrace</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              <span style="color: #000000; font-weight: bold;">return</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #339933;">;</span>
           <span style="color: #009900;">&#125;</span>
       <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #008000; font-style: italic; font-weight: bold;">/** Concrete Prototypes to clone **/</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> CoconutCookie <span style="color: #000000; font-weight: bold;">extends</span> Cookie <span style="color: #009900;">&#123;</span> <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #008000; font-style: italic; font-weight: bold;">/** Client Class**/</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> CookieMachine
    <span style="color: #009900;">&#123;</span>
    &nbsp;
      <span style="color: #000000; font-weight: bold;">private</span> Cookie cookie<span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//cookie必须是可复制的</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">public</span> CookieMachine<span style="color: #009900;">&#40;</span>Cookie cookie<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span> 
            <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">cookie</span> <span style="color: #339933;">=</span> cookie<span style="color: #339933;">;</span> 
        <span style="color: #009900;">&#125;</span> 
        <span style="color: #000000; font-weight: bold;">public</span> Cookie makeCookie<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span> 
          <span style="color: #000000; font-weight: bold;">return</span> <span style="color: #009900;">&#40;</span>Cookie<span style="color: #009900;">&#41;</span>cookie.<span style="color: #006633;">clone</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> 
        <span style="color: #009900;">&#125;</span> 
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #003399;">Object</span> clone<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span> <span style="color: #009900;">&#125;</span> 
    &nbsp;
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">void</span> main<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> args<span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span> 
            Cookie tempCookie <span style="color: #339933;">=</span>  <span style="color: #000066; font-weight: bold;">null</span><span style="color: #339933;">;</span> 
            Cookie prot <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> CoconutCookie<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> 
            CookieMachine cm <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> CookieMachine<span style="color: #009900;">&#40;</span>prot<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">//设置原型</span>
            <span style="color: #000000; font-weight: bold;">for</span><span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> i<span style="color: #339933;">=</span><span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span> i<span style="color: #339933;">&lt;</span><span style="color: #cc66cc;">100</span><span style="color: #339933;">;</span> i<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> 
                tempCookie <span style="color: #339933;">=</span> cm.<span style="color: #006633;">makeCookie</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//通过复制原型返回多个cookie </span>
        <span style="color: #009900;">&#125;</span> 
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">/** Prototype Class **/
    public class Cookie implements Cloneable {
    
       public Object clone()
       {
           try{
               //In an actual implementation of this pattern you would now attach references to
               //the expensive to produce parts from the copies that are held inside the prototype.
               return this.getClass().newInstance();
           }
           catch(InstantiationException e)
           {
              e.printStackTrace();
              return null;
           }
       }
    }
    
    /** Concrete Prototypes to clone **/
    public class CoconutCookie extends Cookie { }
    
    /** Client Class**/
    public class CookieMachine
    {
    
      private Cookie cookie;//cookie必须是可复制的
    
        public CookieMachine(Cookie cookie) { 
            this.cookie = cookie; 
        } 
        public Cookie makeCookie() { 
          return (Cookie)cookie.clone(); 
        } 
        public Object clone() { } 
    
        public static void main(String args[]){ 
            Cookie tempCookie =  null; 
            Cookie prot = new CoconutCookie(); 
            CookieMachine cm = new CookieMachine(prot); //设置原型
            for(int i=0; i&lt;100; i++) 
                tempCookie = cm.makeCookie();//通过复制原型返回多个cookie 
        } 
    }</p></div>
    ";i:6;s:4014:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"> <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> Singleton <span style="color: #009900;">&#123;</span>
        <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000000; font-weight: bold;">volatile</span> Singleton INSTANCE <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #666666; font-style: italic;">// Private constructor suppresses </span>
        <span style="color: #666666; font-style: italic;">// default public constructor</span>
        <span style="color: #000000; font-weight: bold;">private</span> Singleton<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span><span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #666666; font-style: italic;">//thread safe and performance  promote </span>
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span>  Singleton getInstance<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">if</span><span style="color: #009900;">&#40;</span>INSTANCE <span style="color: #339933;">==</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span>
                 <span style="color: #000000; font-weight: bold;">synchronized</span><span style="color: #009900;">&#40;</span>Singleton.<span style="color: #000000; font-weight: bold;">class</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span>
                     <span style="color: #666666; font-style: italic;">//when more than two threads run into the first null check same time, to avoid instanced more than one time, it needs to be checked again.</span>
                     <span style="color: #000000; font-weight: bold;">if</span><span style="color: #009900;">&#40;</span>INSTANCE <span style="color: #339933;">==</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span> 
                         INSTANCE <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Singleton<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                      <span style="color: #009900;">&#125;</span>
                  <span style="color: #009900;">&#125;</span> 
            <span style="color: #009900;">&#125;</span>
            <span style="color: #000000; font-weight: bold;">return</span> INSTANCE<span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;"> public class Singleton {
        private static volatile Singleton INSTANCE = null;
    
        // Private constructor suppresses 
        // default public constructor
        private Singleton() {}
    
        //thread safe and performance  promote 
        public static  Singleton getInstance() {
            if(INSTANCE == null){
                 synchronized(Singleton.class){
                     //when more than two threads run into the first null check same time, to avoid instanced more than one time, it needs to be checked again.
                     if(INSTANCE == null){ 
                         INSTANCE = new Singleton();
                      }
                  } 
            }
            return INSTANCE;
        }
      }</p></div>
    ";i:7;s:3077:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">class</span> Target:
        <span style="color: #ff7700;font-weight:bold;">def</span> Request<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>:
            <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">&quot;common request.&quot;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">class</span> Adaptee<span style="color: black;">&#40;</span>Target<span style="color: black;">&#41;</span>:
        <span style="color: #ff7700;font-weight:bold;">def</span> SpecificRequest<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>:
            <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">&quot;specific request.&quot;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">class</span> Adapter<span style="color: black;">&#40;</span>Target<span style="color: black;">&#41;</span>:
        <span style="color: #ff7700;font-weight:bold;">def</span> <span style="color: #0000cd;">__init__</span><span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: #66cc66;">,</span>ada<span style="color: black;">&#41;</span>:
            <span style="color: #008000;">self</span>.<span style="color: black;">adaptee</span> <span style="color: #66cc66;">=</span> ada
        <span style="color: #ff7700;font-weight:bold;">def</span> Request<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>:
            <span style="color: #008000;">self</span>.<span style="color: black;">adaptee</span>.<span style="color: black;">SpecificRequest</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> __name__ <span style="color: #66cc66;">==</span> <span style="color: #483d8b;">&quot;__main__&quot;</span>:
        adaptee <span style="color: #66cc66;">=</span> Adaptee<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
        adapter <span style="color: #66cc66;">=</span> Adapter<span style="color: black;">&#40;</span>adaptee<span style="color: black;">&#41;</span>
        adapter.<span style="color: black;">Request</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">class Target:
        def Request():
            print &quot;common request.&quot;
    
    class Adaptee(Target):
        def SpecificRequest(self):
            print &quot;specific request.&quot;
    
    class Adapter(Target):
        def __init__(self,ada):
            self.adaptee = ada
        def Request(self):
            self.adaptee.SpecificRequest()
    
    if __name__ == &quot;__main__&quot;:
        adaptee = Adaptee()
        adapter = Adapter(adaptee)
        adapter.Request()</p></div>
    ";i:8;s:8153:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;">组合模式
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">class</span> Component:
        <span style="color: #ff7700;font-weight:bold;">def</span> <span style="color: #0000cd;">__init__</span><span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: #66cc66;">,</span>strName<span style="color: black;">&#41;</span>:
            <span style="color: #008000;">self</span>.<span style="color: black;">m_strName</span> <span style="color: #66cc66;">=</span> strName
        <span style="color: #ff7700;font-weight:bold;">def</span> Add<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: #66cc66;">,</span>com<span style="color: black;">&#41;</span>:
            <span style="color: #ff7700;font-weight:bold;">pass</span>
        <span style="color: #ff7700;font-weight:bold;">def</span> Display<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: #66cc66;">,</span>nDepth<span style="color: black;">&#41;</span>:
            <span style="color: #ff7700;font-weight:bold;">pass</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">class</span> Leaf<span style="color: black;">&#40;</span>Component<span style="color: black;">&#41;</span>:
        <span style="color: #ff7700;font-weight:bold;">def</span> Add<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: #66cc66;">,</span>com<span style="color: black;">&#41;</span>:
            <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">&quot;leaf can't add&quot;</span>
        <span style="color: #ff7700;font-weight:bold;">def</span> Display<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: #66cc66;">,</span>nDepth<span style="color: black;">&#41;</span>:
            strtemp <span style="color: #66cc66;">=</span> <span style="color: #483d8b;">&quot;&quot;</span>
            <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">range</span><span style="color: black;">&#40;</span>nDepth<span style="color: black;">&#41;</span>:
                strtemp<span style="color: #66cc66;">=</span>strtemp+<span style="color: #483d8b;">&quot;-&quot;</span>
            strtemp<span style="color: #66cc66;">=</span>strtemp+<span style="color: #008000;">self</span>.<span style="color: black;">m_strName</span>
            <span style="color: #ff7700;font-weight:bold;">print</span> strtemp
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">class</span> Composite<span style="color: black;">&#40;</span>Component<span style="color: black;">&#41;</span>:
        <span style="color: #ff7700;font-weight:bold;">def</span> <span style="color: #0000cd;">__init__</span><span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: #66cc66;">,</span>strName<span style="color: black;">&#41;</span>:
            <span style="color: #008000;">self</span>.<span style="color: black;">m_strName</span> <span style="color: #66cc66;">=</span> strName
            <span style="color: #008000;">self</span>.<span style="color: black;">c</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#93;</span>
        <span style="color: #ff7700;font-weight:bold;">def</span> Add<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: #66cc66;">,</span>com<span style="color: black;">&#41;</span>:
            <span style="color: #008000;">self</span>.<span style="color: black;">c</span>.<span style="color: black;">append</span><span style="color: black;">&#40;</span>com<span style="color: black;">&#41;</span>
        <span style="color: #ff7700;font-weight:bold;">def</span> Display<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: #66cc66;">,</span>nDepth<span style="color: black;">&#41;</span>:
            strtemp<span style="color: #66cc66;">=</span><span style="color: #483d8b;">&quot;&quot;</span>
            <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">range</span><span style="color: black;">&#40;</span>nDepth<span style="color: black;">&#41;</span>:
                strtemp<span style="color: #66cc66;">=</span>strtemp+<span style="color: #483d8b;">&quot;-&quot;</span>
            strtemp<span style="color: #66cc66;">=</span>strtemp+<span style="color: #008000;">self</span>.<span style="color: black;">m_strName</span>
            <span style="color: #ff7700;font-weight:bold;">print</span> strtemp
            <span style="color: #ff7700;font-weight:bold;">for</span> com <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">self</span>.<span style="color: black;">c</span>:
                com.<span style="color: black;">Display</span><span style="color: black;">&#40;</span>nDepth+<span style="color: #ff4500;">2</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> __name__ <span style="color: #66cc66;">==</span> <span style="color: #483d8b;">&quot;__main__&quot;</span>:
        p <span style="color: #66cc66;">=</span> Composite<span style="color: black;">&#40;</span><span style="color: #483d8b;">&quot;Wong&quot;</span><span style="color: black;">&#41;</span>
        p.<span style="color: black;">Add</span><span style="color: black;">&#40;</span>Leaf<span style="color: black;">&#40;</span><span style="color: #483d8b;">&quot;Lee&quot;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
        p.<span style="color: black;">Add</span><span style="color: black;">&#40;</span>Leaf<span style="color: black;">&#40;</span><span style="color: #483d8b;">&quot;Zhao&quot;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
        p1 <span style="color: #66cc66;">=</span> Composite<span style="color: black;">&#40;</span><span style="color: #483d8b;">&quot;Wu&quot;</span><span style="color: black;">&#41;</span>
        p1.<span style="color: black;">Add</span><span style="color: black;">&#40;</span>Leaf<span style="color: black;">&#40;</span><span style="color: #483d8b;">&quot;San&quot;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
        p.<span style="color: black;">Add</span><span style="color: black;">&#40;</span>p1<span style="color: black;">&#41;</span>
        p.<span style="color: black;">Display</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span><span style="color: #66cc66;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">组合模式
    
    class Component:
        def __init__(self,strName):
            self.m_strName = strName
        def Add(self,com):
            pass
        def Display(self,nDepth):
            pass
    
    class Leaf(Component):
        def Add(self,com):
            print &quot;leaf can't add&quot;
        def Display(self,nDepth):
            strtemp = &quot;&quot;
            for i in range(nDepth):
                strtemp=strtemp+&quot;-&quot;
            strtemp=strtemp+self.m_strName
            print strtemp
    
    class Composite(Component):
        def __init__(self,strName):
            self.m_strName = strName
            self.c = []
        def Add(self,com):
            self.c.append(com)
        def Display(self,nDepth):
            strtemp=&quot;&quot;
            for i in range(nDepth):
                strtemp=strtemp+&quot;-&quot;
            strtemp=strtemp+self.m_strName
            print strtemp
            for com in self.c:
                com.Display(nDepth+2)
    
    if __name__ == &quot;__main__&quot;:
        p = Composite(&quot;Wong&quot;)
        p.Add(Leaf(&quot;Lee&quot;))
        p.Add(Leaf(&quot;Zhao&quot;))
        p1 = Composite(&quot;Wu&quot;)
        p1.Add(Leaf(&quot;San&quot;))
        p.Add(p1)
        p.Display(1);</p></div>
    ";i:9;s:15097:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.util.List</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.util.ArrayList</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;">/* The Command interface */</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">interface</span> Command <span style="color: #009900;">&#123;</span>
       <span style="color: #000066; font-weight: bold;">void</span> execute<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;">/* The Invoker class */</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> <span style="color: #000000; font-weight: bold;">Switch</span> <span style="color: #009900;">&#123;</span>
       <span style="color: #000000; font-weight: bold;">private</span> List<span style="color: #339933;">&lt;</span>Command<span style="color: #339933;">&gt;</span> history <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> ArrayList<span style="color: #339933;">&lt;</span>Command<span style="color: #339933;">&gt;</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
       <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">Switch</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
       <span style="color: #009900;">&#125;</span>
    &nbsp;
       <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> storeAndExecute<span style="color: #009900;">&#40;</span>Command cmd<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">history</span>.<span style="color: #006633;">add</span><span style="color: #009900;">&#40;</span>cmd<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// optional </span>
          cmd.<span style="color: #006633;">execute</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>        
       <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;">/* The Receiver class */</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> Light <span style="color: #009900;">&#123;</span>
       <span style="color: #000000; font-weight: bold;">public</span> Light<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
       <span style="color: #009900;">&#125;</span>
    &nbsp;
       <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> turnOn<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;The light is on&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
       <span style="color: #009900;">&#125;</span>
    &nbsp;
       <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> turnOff<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;The light is off&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
       <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;">/* The Command for turning on the light - ConcreteCommand #1 */</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> FlipUpCommand <span style="color: #000000; font-weight: bold;">implements</span> Command <span style="color: #009900;">&#123;</span>
       <span style="color: #000000; font-weight: bold;">private</span> Light theLight<span style="color: #339933;">;</span>
    &nbsp;
       <span style="color: #000000; font-weight: bold;">public</span> FlipUpCommand<span style="color: #009900;">&#40;</span>Light light<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">theLight</span> <span style="color: #339933;">=</span> light<span style="color: #339933;">;</span>
       <span style="color: #009900;">&#125;</span>
    &nbsp;
       <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> execute<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span>
          theLight.<span style="color: #006633;">turnOn</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
       <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;">/* The Command for turning off the light - ConcreteCommand #2 */</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> FlipDownCommand <span style="color: #000000; font-weight: bold;">implements</span> Command <span style="color: #009900;">&#123;</span>
       <span style="color: #000000; font-weight: bold;">private</span> Light theLight<span style="color: #339933;">;</span>
    &nbsp;
       <span style="color: #000000; font-weight: bold;">public</span> FlipDownCommand<span style="color: #009900;">&#40;</span>Light light<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">theLight</span> <span style="color: #339933;">=</span> light<span style="color: #339933;">;</span>
       <span style="color: #009900;">&#125;</span>
    &nbsp;
       <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> execute<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          theLight.<span style="color: #006633;">turnOff</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
       <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;">/* The test class or client */</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> PressSwitch <span style="color: #009900;">&#123;</span>
       <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">void</span> main<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> args<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span>
          Light lamp <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Light<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          Command switchUp <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> FlipUpCommand<span style="color: #009900;">&#40;</span>lamp<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          Command switchDown <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> FlipDownCommand<span style="color: #009900;">&#40;</span>lamp<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
          <span style="color: #000000; font-weight: bold;">Switch</span> mySwitch <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #000000; font-weight: bold;">Switch</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
          <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
             <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;ON&quot;</span>.<span style="color: #006633;">equalsIgnoreCase</span><span style="color: #009900;">&#40;</span>args<span style="color: #009900;">&#91;</span><span style="color: #cc66cc;">0</span><span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                mySwitch.<span style="color: #006633;">storeAndExecute</span><span style="color: #009900;">&#40;</span>switchUp<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
             <span style="color: #009900;">&#125;</span>
             <span style="color: #000000; font-weight: bold;">else</span> <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;OFF&quot;</span>.<span style="color: #006633;">equalsIgnoreCase</span><span style="color: #009900;">&#40;</span>args<span style="color: #009900;">&#91;</span><span style="color: #cc66cc;">0</span><span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                mySwitch.<span style="color: #006633;">storeAndExecute</span><span style="color: #009900;">&#40;</span>switchDown<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
             <span style="color: #009900;">&#125;</span>
             <span style="color: #000000; font-weight: bold;">else</span> <span style="color: #009900;">&#123;</span>
                <span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Argument <span style="color: #000099; font-weight: bold;">\&quot;</span>ON<span style="color: #000099; font-weight: bold;">\&quot;</span> or <span style="color: #000099; font-weight: bold;">\&quot;</span>OFF<span style="color: #000099; font-weight: bold;">\&quot;</span> is required.&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
             <span style="color: #009900;">&#125;</span>
          <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">Exception</span> e<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
             <span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Arguments required.&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span>
       <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">import java.util.List;
    import java.util.ArrayList;
    
    /* The Command interface */
    public interface Command {
       void execute();
    }
    
    /* The Invoker class */
    public class Switch {
       private List&lt;Command&gt; history = new ArrayList&lt;Command&gt;();
    
       public Switch() {
       }
    
       public void storeAndExecute(Command cmd) {
          this.history.add(cmd); // optional 
          cmd.execute();        
       }
    }
    
    /* The Receiver class */
    public class Light {
       public Light() {
       }
    
       public void turnOn() {
          System.out.println(&quot;The light is on&quot;);
       }
    
       public void turnOff() {
          System.out.println(&quot;The light is off&quot;);
       }
    }
    
    /* The Command for turning on the light - ConcreteCommand #1 */
    public class FlipUpCommand implements Command {
       private Light theLight;
    
       public FlipUpCommand(Light light) {
          this.theLight = light;
       }
    
       public void execute(){
          theLight.turnOn();
       }
    }
    
    /* The Command for turning off the light - ConcreteCommand #2 */
    public class FlipDownCommand implements Command {
       private Light theLight;
    
       public FlipDownCommand(Light light) {
          this.theLight = light;
       }
    
       public void execute() {
          theLight.turnOff();
       }
    }
    
    /* The test class or client */
    public class PressSwitch {
       public static void main(String[] args){
          Light lamp = new Light();
          Command switchUp = new FlipUpCommand(lamp);
          Command switchDown = new FlipDownCommand(lamp);
    
          Switch mySwitch = new Switch();
    
          try {
             if (&quot;ON&quot;.equalsIgnoreCase(args[0])) {
                mySwitch.storeAndExecute(switchUp);
             }
             else if (&quot;OFF&quot;.equalsIgnoreCase(args[0])) {
                mySwitch.storeAndExecute(switchDown);
             }
             else {
                System.out.println(&quot;Argument \&quot;ON\&quot; or \&quot;OFF\&quot; is required.&quot;);
             }
          } catch (Exception e) {
             System.out.println(&quot;Arguments required.&quot;);
          }
       }
    }</p></div>
    ";}
categories:
  - 电脑知识
tags:
  - 设计模式

---
## 设计模式学习

<!--more-->

## 抽象工厂模式

**场景：** 把同一主题的工厂封装起来，对外提供一致的接口，返回不同的产品。
**使用：**利用接口建立一个抽象工厂，不同的工厂实现这个接口，产出的产品也要有一个接口。在使用时，需要选择具体工厂类（不能new 接口）。
**实例：**提供对不同的数据库访问的支持。IUser和IDepartment是两种不同的抽象产品，它们都有Access和SQL Server这两种不同的实现；IFactory是产生IUser和IDepartment的抽象工厂，根据具体实现（AccessFactory和SqlFactory）产生对应的具体的对象（CAccessUser与CAccessDepartment，或者CSqlUser与CSqlDepartment）。
![File:Abstract factory UML.svg][1] 
<pre lang="python" escaped="true">抽象工厂模式（python）

class IUser:
    def GetUser(self):
        pass

class IDepartment:
    def GetDepartment(self):
        pass

class CAccessUser(IUser):
    def GetUser(self):
        print "Access GetUser"

class CAccessDepartment(IDepartment):
    def GetDepartment(self):
        print "Access GetDepartment"

class CSqlUser(IUser):
    def GetUser(self):
        print "Sql GetUser"

class CSqlDepartment(IDepartment):
    def GetDepartment(self):
        print "Sql GetDepartment"

class IFactory:
    def CreateUser(self):
        pass
    def CreateDepartment(self):
        pass

class AccessFactory(IFactory):
    def CreateUser(self):
        temp=CAccessUser()
        return temp
    def CreateDepartment(self):
        temp = CAccessDepartment()
        return temp

class SqlFactory(IFactory):
    def CreateUser(self):
        temp = CSqlUser()
        return temp
    def CreateDepartment(self):
        temp = CSqlDepartment()
        return temp

if __name__ == "__main__":
    factory = SqlFactory()
    user=factory.CreateUser()
    depart=factory.CreateDepartment()
    user.GetUser()
    depart.GetDepartment()</pre>
## 工厂方法模式/简单工厂

**场景：**创建实体类比较多，抽取出来，根据条件判断要创建哪个实现类。
**使用：**根据不同的参数选择具体的实现类。
**实例：**一个程序要读取图像文件。程序支持多种图像格式，每种格式都有一个对应的`ImageReader`类用来读取图像。程序每次读取图像时，需要基于文件信息创建合适类型的`ImageReader`。
&nbsp;
![][2] 
<pre lang="java" escaped="true">public class ImageReaderFactory {
    public static ImageReader imageReaderFactoryMethod(InputStream is) {
        ImageReader product = null;

        int imageType = determineImageType(is);
        switch (imageType) {
            case ImageReaderFactory.GIF:
                product = new GifReader(is);
            case ImageReaderFactory.JPEG:
                product = new JpegReader(is);
            //...
        }
        return product;
    }
}</pre>
## 生成器模式/**建造者模式**

**场景：**和抽象工厂类似，创建复杂的对象。生成器着重在一步一步的构造对象。
**使用：**一个Builder抽象类，一个实现Builder类，有多个方法来构造对象。Director是用来使用builder的。
**实例：**制造Pizza
![][3] 
<pre lang="java" escaped="true">/** "Product" */
 class Pizza {
   private String dough = "";
   private String sauce = "";
   private String topping = "";

   public void setDough (String dough)     { this.dough = dough; }
   public void setSauce (String sauce)     { this.sauce = sauce; }
   public void setTopping (String topping) { this.topping = topping; }
 }

 ''/** "Abstract Builder" */''
 abstract class PizzaBuilder {
   protected Pizza pizza;

   public Pizza getPizza() { return pizza; }
   public void createNewPizzaProduct() { pizza = new Pizza(); }

   public abstract void buildDough();
   public abstract void buildSauce();
   public abstract void buildTopping();
 }

 /** "ConcreteBuilder" */
 class HawaiianPizzaBuilder extends PizzaBuilder {
   public void buildDough()   { pizza.setDough("cross"); }
   public void buildSauce()   { pizza.setSauce("mild"); }
   public void buildTopping() { pizza.setTopping("ham+pineapple"); }
 }

 /** "ConcreteBuilder" */
 class SpicyPizzaBuilder extends PizzaBuilder {
   public void buildDough()   { pizza.setDough("pan baked"); }
   public void buildSauce()   { pizza.setSauce("hot"); }
   public void buildTopping() { pizza.setTopping("pepperoni+salami"); }
 }

 ''/** "Director" */''
 class Waiter {
   private PizzaBuilder pizzaBuilder;

   public void setPizzaBuilder (PizzaBuilder pb) { pizzaBuilder = pb; }
   public Pizza getPizza() { return pizzaBuilder.getPizza(); }

   public void constructPizza() {
     pizzaBuilder.createNewPizzaProduct();
     pizzaBuilder.buildDough();
     pizzaBuilder.buildSauce();
     pizzaBuilder.buildTopping();
   }
 }

 /** A customer ordering a pizza. */
 class BuilderExample {
   public static void main(String[] args) {
     Waiter waiter = new Waiter();
     PizzaBuilder hawaiian_pizzabuilder = new HawaiianPizzaBuilder();
     PizzaBuilder spicy_pizzabuilder = new SpicyPizzaBuilder();

     waiter.setPizzaBuilder ( hawaiian_pizzabuilder );
     waiter.constructPizza();

     Pizza pizza = waiter.getPizza();
   }
 }</pre>
&nbsp;
<h2 id="firstHeading" lang="zh-CN">  惰性初始模式/惰性工厂</h2>
**场景：**延迟创建对象
**使用：**有一个map来存储创建出来的对象，如果没创建过就创建出来放到map里，否则直接返回。要注意要有锁。
<pre lang="java" escaped="true">import java.util.*;

public class Fruit
{
    private static final Map&lt;String,Fruit&gt; types = new HashMap&lt;String,Fruit&gt;();
    private final String type;

    // using a private constructor to force use of the factory method.
    private Fruit(String type) {
      this.type = type;
    }

    /**
     * Lazy Factory method, gets the Fruit instance associated with a
     * certain type. Instantiates new ones as needed.
     * @param type Any string that describes a fruit type, e.g. "apple"
     * @return The Fruit instance associated with that type.
     */
    public static synchronized Fruit getFruit(String type) {
      if(!types.containsKey(type))
        types.put(type, new Fruit(type)); // Lazy initialization
      return types.get(type);
    }
}</pre>
## 

## 对象池模式

**场景：**创建实例的时间比较长
**使用：**一开始创建多个实例保存起来，每次用完之后还回池里。
## 

## 原型模式

**场景：**创建实例的成本比较高，复制实例的成本低。
使用：实现clone()这个方法，每个对象可以从自身克隆。python可以使用deepcopy()方法来拷贝。
![][4] 
&nbsp;
<pre lang="java" escaped="true">/** Prototype Class **/
public class Cookie implements Cloneable {

   public Object clone()
   {
       try{
           //In an actual implementation of this pattern you would now attach references to
           //the expensive to produce parts from the copies that are held inside the prototype.
           return this.getClass().newInstance();
       }
       catch(InstantiationException e)
       {
          e.printStackTrace();
          return null;
       }
   }
}

/** Concrete Prototypes to clone **/
public class CoconutCookie extends Cookie { }

/** Client Class**/
public class CookieMachine
{

  private Cookie cookie;//cookie必须是可复制的

    public CookieMachine(Cookie cookie) { 
        this.cookie = cookie; 
    } 
    public Cookie makeCookie() { 
      return (Cookie)cookie.clone(); 
    } 
    public Object clone() { } 

    public static void main(String args[]){ 
        Cookie tempCookie =  null; 
        Cookie prot = new CoconutCookie(); 
        CookieMachine cm = new CookieMachine(prot); //设置原型
        for(int i=0; i&lt;100; i++) 
            tempCookie = cm.makeCookie();//通过复制原型返回多个cookie 
    } 
}</pre>
&nbsp;
## 单例模式

**场景：**只需要创建一个实例，多个使用
**使用：**要注意[Java 中的双重检查（Double-Check）][5]，可以使用在成员变量初始化、使用volatile变量、对方法sync
python单例例子：<http://blog.csdn.net/ghostfromheaven/article/details/7671853>，python的模块（module）本身是单例的
<pre lang="java" escaped="true">public class Singleton {
    private static volatile Singleton INSTANCE = null;

    // Private constructor suppresses 
    // default public constructor
    private Singleton() {}

    //thread safe and performance  promote 
    public static  Singleton getInstance() {
        if(INSTANCE == null){
             synchronized(Singleton.class){
                 //when more than two threads run into the first null check same time, to avoid instanced more than one time, it needs to be checked again.
                 if(INSTANCE == null){ 
                     INSTANCE = new Singleton();
                  }
              } 
        }
        return INSTANCE;
    }
  }</pre>
## 

## 适配器模式

**场景：**和客户需要的接口有差异
**使用：**构建一个Adapter实现客户需要的接口，把对应的方法映射到自己的类上（Adaptee）
![][6] 
<pre lang="python" escaped="true">class Target:
    def Request():
        print "common request."

class Adaptee(Target):
    def SpecificRequest(self):
        print "specific request."

class Adapter(Target):
    def __init__(self,ada):
        self.adaptee = ada
    def Request(self):
        self.adaptee.SpecificRequest()

if __name__ == "__main__":
    adaptee = Adaptee()
    adapter = Adapter(adaptee)
    adapter.Request()</pre>
&nbsp;
## 桥接模式 /Bridge

**场景：**把抽象（abstraction）和实现（implementor）分离，两者可以独立变化
**使用：**Refined Abstraction是为了调用具体实现类
**实例：**不同的汽车有不同的引擎
参考代码见这里：<http://blog.csdn.net/shaopeng5211/article/details/8827507>
![][7] 
&nbsp;
## 组合模式

**场景：**把多个对象组成树状结构来表示局部与整体，这样用户可以一样的对待单个对象和对象的组合。
**实例：**公司人员结构
![][8] 
<pre lang="python" escaped="true">组合模式

class Component:
    def __init__(self,strName):
        self.m_strName = strName
    def Add(self,com):
        pass
    def Display(self,nDepth):
        pass

class Leaf(Component):
    def Add(self,com):
        print "leaf can't add"
    def Display(self,nDepth):
        strtemp = ""
        for i in range(nDepth):
            strtemp=strtemp+"-"
        strtemp=strtemp+self.m_strName
        print strtemp

class Composite(Component):
    def __init__(self,strName):
        self.m_strName = strName
        self.c = []
    def Add(self,com):
        self.c.append(com)
    def Display(self,nDepth):
        strtemp=""
        for i in range(nDepth):
            strtemp=strtemp+"-"
        strtemp=strtemp+self.m_strName
        print strtemp
        for com in self.c:
            com.Display(nDepth+2)

if __name__ == "__main__":
    p = Composite("Wong")
    p.Add(Leaf("Lee"))
    p.Add(Leaf("Zhao"))
    p1 = Composite("Wu")
    p1.Add(Leaf("San"))
    p.Add(p1)
    p.Display(1);</pre>
&nbsp;
## **装饰模式/Decorator**

装饰（ Decorator ）模式又叫做包装模式。通过一种对客户端透明的方式来扩展对象的功能，是继承关系的一个替换方案。
**场景：**对类扩展方法
**代码：**<http://blog.csdn.net/shaopeng5211/article/details/8803120>
![][9] 
&nbsp;
## 外观模式/Facadec

**场景：**为client提供简单的方法，调用具体的多个实现类
**代码**：<http://blog.csdn.net/shaopeng5211/article/details/8813135>
![][10] 
&nbsp;
## 享元模式/Flyweight

采用一个共享来避免大量拥有相同内容对象的开销。这种开销中最常见、直观的就是内存的损耗。享元模式以共享的方式高效的支持大量的细粒度对象。
** **
## 代理模式/Proxy

所谓代理，是指具有与代理元（被代理的对象）具有相同的接口的类，客户端必须通过代理与被代理的目标类交互，而代理一般在交互的过程中（交互前后），进行某些特别的处理。
需要与继承区分，继承是静态的增加方法，代理可以实现一些纵切的功能。
![][11] 
&nbsp;
<h2 id="firstHeading" lang="zh-CN">  职责链模式/Chain of Responsibility</h2>
该模式构造一系列分别担当不同的职责的类的对象来共同完成一个任务，这些类的对象之间像链条一样紧密相连，所以被称作职责链模式。
**场景：**如一件事需要多个部门处理，这个部门处理完交给下个部门。
**使用：**每个对象设定下一个处理的对象是什么，并且在handle方法里调用下一个处理的方法。
**代码：**<http://blog.csdn.net/shaopeng5211/article/details/8857776>
&nbsp;
## 命令模式/Command

命令物件可以把行动(action) 及其参数封装起来，可以重复执行、取消。
![Command Design Pattern Class Diagram.png][12] 
Command                           Command抽象类。  
ConcreteCommand        Command的具体实现类。  
Receiver                             需要被调用的目标对象。  
Invorker                             通过Invorker执行Command对象。
<pre lang="java" escaped="true">import java.util.List;
import java.util.ArrayList;

/* The Command interface */
public interface Command {
   void execute();
}

/* The Invoker class */
public class Switch {
   private List&lt;Command&gt; history = new ArrayList&lt;Command&gt;();

   public Switch() {
   }

   public void storeAndExecute(Command cmd) {
      this.history.add(cmd); // optional 
      cmd.execute();        
   }
}

/* The Receiver class */
public class Light {
   public Light() {
   }

   public void turnOn() {
      System.out.println("The light is on");
   }

   public void turnOff() {
      System.out.println("The light is off");
   }
}

/* The Command for turning on the light - ConcreteCommand #1 */
public class FlipUpCommand implements Command {
   private Light theLight;

   public FlipUpCommand(Light light) {
      this.theLight = light;
   }

   public void execute(){
      theLight.turnOn();
   }
}

/* The Command for turning off the light - ConcreteCommand #2 */
public class FlipDownCommand implements Command {
   private Light theLight;

   public FlipDownCommand(Light light) {
      this.theLight = light;
   }

   public void execute() {
      theLight.turnOff();
   }
}

/* The test class or client */
public class PressSwitch {
   public static void main(String[] args){
      Light lamp = new Light();
      Command switchUp = new FlipUpCommand(lamp);
      Command switchDown = new FlipDownCommand(lamp);

      Switch mySwitch = new Switch();

      try {
         if ("ON".equalsIgnoreCase(args[0])) {
            mySwitch.storeAndExecute(switchUp);
         }
         else if ("OFF".equalsIgnoreCase(args[0])) {
            mySwitch.storeAndExecute(switchDown);
         }
         else {
            System.out.println("Argument \"ON\" or \"OFF\" is required.");
         }
      } catch (Exception e) {
         System.out.println("Arguments required.");
      }
   }
}</pre>
&nbsp;
## 解释器模式/Interpreter

它建立一个解释器，对于特定的计算机程序设计语言，用来解释预先定义的文法。简单地说，Interpreter模式是一种简单的语法解释器构架。
![][13] 
Context 解释器上下文环境类。用来存储解释器的上下文环境，比如需要解释的文法等。  
AbstractExpression 解释器抽象类。  
ConcreteExpression 解释器具体实现类
**代码：**<http://blog.csdn.net/shaopeng5211/article/details/8847991>
&nbsp;
## 迭代器

提供一种方法顺序访问一个聚合对象中各个元素, 而又不需暴露该对象的内部表示。
&nbsp;
## 中介者模式

**场景：**有多个类需要交互，由中介来调用他们。但中介者会变得复杂。
<http://haolloyin.blog.51cto.com/1177454/333810>
&nbsp;
## 备忘录模式

用另一个结构一样的类把变量存储起来。。o(╯□╰)o，可以在某个时间还原。
<http://blog.csdn.net/shaopeng5211/article/details/8879519>
&nbsp;
## 观察者模式

**场景：**一个目标对象管理所有相依于它的观察者对象，并且在它本身的状态改变时主动发出通知。
**使用：**Subject提供注册、删除、通知的方法，Observer注册到Subject，Subject状态变化时，就会通知所有注册的Observer。
**代码：**<a href="http://zh.wikipedia.org/wiki/观察者模式" target="_blank">http://zh.wikipedia.org/wiki/观察者模式</a>
![Observer-pattern-class-diagram.png][14] 
&nbsp;
&nbsp;
## 状态模式

State模式允许通过改变对象的内部状态而改变对象的行为，这个对象表现得就好像修改了它的类一样。
**使用：**Context维护一个state变量，并且使用这个state的方法。但state变更时，方法自然也变了。
![][15] 
&nbsp;
&nbsp;
## 策略模式

策略模式作为一种[软件设计模式][16]，指对象有某个行为，但是在不同的场景中，该行为有不同的实现算法。比如每个人都要“交个人所得税”，但是“在美国交个人所得税”和“在中国交个人所得税”就有不同的算税方法。
**使用：**新建不同的策略让Context调用，需要与状态模式区分，状态模式的迁移对客户是透明的。
![][17] 
&nbsp;
## 模板模式

**模板方法模式**定义了一个[算法][18]的步骤，并允许次类别为一个或多个步骤提供其实践方式。
<a href="http://zh.wikipedia.org/wiki/模板模式" target="_blank">http://zh.wikipedia.org/wiki/模板模式</a>
&nbsp;
## 访问者模式

把对象和算法分开，通过使用回调的方式。对象实现accept方法，传入vistor调用它的方法。
<a href="http://zh.wikipedia.org/wiki/访问者模式" target="_blank">http://zh.wikipedia.org/wiki/访问者模式</a>
![File:Visitor UML class diagram.svg][19] 
## 参考

<http://www.cnblogs.com/wuyuegb2312/archive/2013/04/09/3008320.html>
[http://blog.csdn.net/shaopeng5211/][20]
[http://zh.wikipedia.org/zh-cn/设计模式_(计算机)][21]

 [1]: http://upload.wikimedia.org/wikipedia/commons/thumb/9/9d/Abstract_factory_UML.svg/677px-Abstract_factory_UML.svg.png
 [2]: http://upload.wikimedia.org/wikipedia/commons/thumb/a/a3/FactoryMethod.svg/300px-FactoryMethod.svg.png
 [3]: http://images.cnblogs.com/cnblogs_com/wuyuegb2312/468244/o_ch9.%e5%bb%ba%e9%80%a0%e8%80%85%e6%a8%a1%e5%bc%8f.png
 [4]: http://images.cnblogs.com/cnblogs_com/wuyuegb2312/468244/o_ch6.%e5%8e%9f%e5%9e%8b%e6%a8%a1%e5%bc%8f.png
 [5]: http://blog.csdn.net/dl88250/article/details/5439024
 [6]: http://images.cnblogs.com/cnblogs_com/wuyuegb2312/468244/o_ch13.%e9%80%82%e9%85%8d%e5%99%a8%e6%a8%a1%e5%bc%8f.png
 [7]: http://images.cnblogs.com/cnblogs_com/wuyuegb2312/468244/o_ch18.%e6%a1%a5%e6%8e%a5%e6%a8%a1%e5%bc%8f.png
 [8]: http://images.cnblogs.com/cnblogs_com/wuyuegb2312/468244/o_ch15.%e7%bb%84%e5%90%88%e6%a8%a1%e5%bc%8f.png
 [9]: http://images.cnblogs.com/cnblogs_com/wuyuegb2312/468244/o_ch3.%e8%a3%85%e9%a5%b0%e6%a8%a1%e5%bc%8f.png
 [10]: http://img.my.csdn.net/uploads/201304/17/1366170463_6144.png
 [11]: http://images.cnblogs.com/cnblogs_com/wuyuegb2312/468244/o_ch.4%e4%bb%a3%e7%90%86%e6%a8%a1%e5%bc%8f.png
 [12]: http://upload.wikimedia.org/wikipedia/commons/8/8e/Command_Design_Pattern_Class_Diagram.png
 [13]: http://img.my.csdn.net/uploads/201304/25/1366854216_4860.png
 [14]: http://upload.wikimedia.org/wikipedia/commons/e/e2/Observer-pattern-class-diagram.png
 [15]: http://img.blog.csdn.net/20130504100850466
 [16]: http://zh.wikipedia.org/wiki/%E8%BB%9F%E4%BB%B6%E8%A8%AD%E8%A8%88%E6%A8%A1%E5%BC%8F "软件设计模式"
 [17]: http://upload.wikimedia.org/wikipedia/commons/thumb/4/4c/Strategy_Pattern_Diagram_ZP.svg/500px-Strategy_Pattern_Diagram_ZP.svg.png
 [18]: http://zh.wikipedia.org/wiki/%E6%BC%94%E7%AE%97%E6%B3%95 "算法"
 [19]: http://upload.wikimedia.org/wikipedia/commons/thumb/b/b1/Visitor_UML_class_diagram.svg/624px-Visitor_UML_class_diagram.svg.png
 [20]: http://blog.csdn.net/shaopeng5211
 [21]: http://zh.wikipedia.org/zh-cn/设计模式_(计算机) "http://zh.wikipedia.org/zh-cn/设计模式_(计算机)"
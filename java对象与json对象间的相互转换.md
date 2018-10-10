# [java对象与json对象间的相互转换](https://www.cnblogs.com/sharpest/p/7844533.html)

### 1.简单的解析json字符串

首先将json字符串转换为json对象，然后再解析json对象，过程如下。

JSONObject jsonObject = JSONObject.fromObject(jsonStr);

根据json中的键得到它的值

String name = jsonObject.getString("name");
int num = jsonObject.getInt("num");
String sex = jsonObject.getString("sex");
int age = jsonObject.getInt("age");

### 2.将json字符串转换为java对象

同样先将json字符串转换为json对象，再将json对象转换为java对象，如下所示。

JSONObject obj = new JSONObject().fromObject(jsonStr);//将json字符串转换为json对象

将json对象转换为java对象

Person jb = (Person)JSONObject.toBean(obj,Person.class);//将建json对象转换为Person对象

### 3.将java对象转换为json字符串

先将java对象转换为json对象，在将json对象转换为json字符串

JSONObject json = JSONObject.fromObject(obj);//将java对象转换为json对象

String str = json.toString();//将json对象转换为字符串



完整代码如下：

	package baz.parse;
	
	import java.util.ArrayList;
	import java.util.List;
	
	import net.sf.json.JSON;
	import net.sf.json.JSONArray;
	import net.sf.json.JSONObject;
	import net.sf.json.JSONSerializer;
	import baz.bean.Person;
	
	public class ParseJson {
	private String jsonStr;
	
	public ParseJson() {	
	}
	public ParseJson(String str){
		this.jsonStr = str;
	}
	/**
	 * 解析json字符串
	 */
	public void parse(){
		JSONObject jsonObject = JSONObject.fromObject(jsonStr);
		String name = jsonObject.getString("name");
		int num = jsonObject.getInt("num");
		String sex = jsonObject.getString("sex");
		int age = jsonObject.getInt("age");
		
		System.out.println(name + " " + num + " " + sex + " " + age);
	}
	//将json字符串转换为java对象
	public Person JSON2Object(){
		//接收{}对象，此处接收数组对象会有异常
		if(jsonStr.indexOf("[") != -1){
			jsonStr = jsonStr.replace("[", "");
		}
		if(jsonStr.indexOf("]") != -1){
			jsonStr = jsonStr.replace("]", "");
		}
		JSONObject obj = new JSONObject().fromObject(jsonStr);//将json字符串转换为json对象
		Person jb = (Person)JSONObject.toBean(obj,Person.class);//将建json对象转换为Person对象
		return jb;//返回一个Person对象
	}
	}
	package baz.bean;
	
	public class Person {
	    private String name;
	    private int num;
	    private String sex;
	    private int age;
	
	    public Person() {
	        // TODO Auto-generated constructor stub
	    }
	
	    public Person(String name, int num, String sex, int age) {
	        super();
	        this.name = name;
	        this.num = num;
	        this.sex = sex;
	        this.age = age;
	    }
	    public String getName() {
	        return name;
	    }
	
	    public void setName(String name) {
	        this.name = name;
	    }
	
	    public int getNum() {
	        return num;
	    }
	
	    public void setNum(int num) {
	        this.num = num;
	    }
	
	    public String getSex() {
	        return sex;
	    }
	
	    public void setSex(String sex) {
	        this.sex = sex;
	    }
	
	    public int getAge() {
	        return age;
	    }
	
	    public void setAge(int age) {
	        this.age = age;
	    }
	}

 将java对象转换为json字符串


	package baz.cons;
	 
	 
	import net.sf.json.JSONObject;
	 
	 
	/**
	 * 将java对象转换为json字符串
	 * @author Administrator
	 *
	 */
	public class ConsJson {
		
		public ConsJson() {
			// TODO Auto-generated constructor stub
		}
		
		public String Object2Json(Object obj){
			JSONObject json = JSONObject.fromObject(obj);//将java对象转换为json对象
			String str = json.toString();//将json对象转换为字符串
			
			return str;
		}
	}
	

测试类：	

	package baz.test;
	
	import java.util.List;
	
	import baz.bean.Person;
	import baz.cons.ConsJson;
	import baz.parse.ParseJson;
	
	public class Test {
		public static void main(String[] args) {
	    //将字符串转换为json对象，然后根据建得到相应的值
	        ParseJson pj = new ParseJson("		{\"name\":\"gu\",\"num\":123456,\"sex\":\"male\",\"age\":24}");
	        pj.parse();
	
	        //将一个json字符串转换为java对象
	        Person p = pj.JSON2Object();
	        System.out.println("Name:" + p.getName());
	        System.out.println("Num:" + p.getNum());
	        System.out.println("Sex:" + p.getSex());
	        System.out.println("age:" + p.getAge());
	
	        //将一个java对象转换为Json字符串
	        Person p1 = new Person("gu1",123,"male",23);
	        ConsJson cj = new ConsJson();
	        String str1 = cj.Object2Json(p1);
	        System.out.println(str1);
	
	    }
	}

测试输出如下：
gu 123456 male 24
Name:gu
Num:123456
Sex:male
age:24
{"age":23,"name":"gu1","num":123,"sex":"male"}
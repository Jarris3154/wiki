### Snmp Agent Simulator

1. ireasoning 官网下载最新的SNMP Agent Simulator
2. 从下载的程序中找到lib/目录下的simulator.jar
3. 使用依赖 javassist 修改其中的字节码，可以使用 [jclasslib](https://github.com/ingokegel/jclasslib/releases) 的Viewer辅助查看字节码。
   
```xml
        <dependency>
            <groupId>org.javassist</groupId>
            <artifactId>javassist</artifactId>
            <version>3.21.0-GA</version>
        </dependency>
```
主要是使用CtBehavior的方法setBody()或insertAt等方法替换代码。（注：增加的代码中要引用的类，最好是使用Full Qualified Name来写）

   ```java
    package com.yjy.cloudplatform.autodeploy.crackSimulator;


import javassist.ClassPool;
import javassist.CtBehavior;
import javassist.CtClass;

/**
 * ReplaceClassFile
 *
 * @author Jarris
 * 2021-02-02
 **/
public class CrackSnmpAgentSimulator {
    public static void main(String[] args) throws Exception {

        String isEval = "IS_EVAL=false;";
        replaceClass("C:\\Users\\admin\\Desktop", "com.ireasoning.util.gc", 1, isEval, 70);

        replaceSimMainFrame("C:\\Users\\admin\\Desktop", "com.ireasoning.ui.SimMainFrame", 7);

        String body = "{return false;}";
        replaceMethodBody("C:\\Users\\admin\\Desktop", "com.ireasoning.ui.we", 8, body);
    }

    private static void replaceClass(String path, String classFullName, int methodIndex, String code, int line) throws Exception{
        ClassPool pool = ClassPool.getDefault();
        //设置目标类的路径
        pool.insertClassPath(path);
        //获得要修改的类
        CtClass ctClass = pool.get(classFullName);
        //得到类初始化方法

        CtBehavior[] declaredBehaviors = ctClass.getDeclaredBehaviors();
        CtBehavior method = declaredBehaviors[methodIndex];

        method.insertAt(line, code);
        ctClass.writeFile();
    }

    private static void replaceSimMainFrame(String path, String classFullName, int methodIndex) throws Exception{
        String setJ = "j=false;";
        String isFree = "System.out.println(\"isFree: \"+com.ireasoning.protocol.snmp.uc.IS_FREE);";

        ClassPool pool = ClassPool.getDefault();
        //设置目标类的路径
        pool.insertClassPath(path);
        //获得要修改的类
        CtClass ctClass = pool.get(classFullName);
        //得到类初始化方法

        CtBehavior[] declaredBehaviors = ctClass.getDeclaredBehaviors();
        CtBehavior method = declaredBehaviors[methodIndex];
        method.insertAt(0, isFree);
        method.insertAt(102, setJ);

        CtBehavior methodA = declaredBehaviors[3];
        methodA.setBody("{}");
        CtBehavior methodB = declaredBehaviors[14];
        CtBehavior methodC = declaredBehaviors[15];
        CtBehavior methodD = declaredBehaviors[16];
        //methodA.insertAt(0, "System.out.println(\"enter a()... IS_EVAL: \"+ com.ireasoning.util.gc.IS_EVAL);");
        methodB.insertAt(0, "System.out.println(\"enter b()...\");");
        methodC.insertAt(0, "System.out.println(\"enter c()...\");");
        methodD.insertAt(0, "System.out.println(\"enter d()... IS_EVAL: \"+ com.ireasoning.util.gc.IS_EVAL);");
        ctClass.writeFile();
    }

    private static void replaceMethodBody(String path, String classFullName, int methodIndex, String code) throws Exception{
        ClassPool pool = ClassPool.getDefault();
        //设置目标类的路径
        pool.insertClassPath(path);
        //获得要修改的类
        CtClass ctClass = pool.get(classFullName);
        //得到类初始化方法
        CtBehavior[] declaredBehaviors = ctClass.getDeclaredBehaviors();
        CtBehavior method = declaredBehaviors[methodIndex];

        method.setBody(code);
        ctClass.writeFile();
    }
}

   ```
4. 然后simulator.jar中对应的class文件替换。
5. 将simulator.jar替换到lib/目录下，大功告成！


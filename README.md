# mybatis-expands-generator

使用方式可以参考下面示例
pom.xml 添加下面信息

    <build>
        <plugins>
            <plugin>
                <groupId>org.mybatis.generator</groupId>
                <artifactId>mybatis-generator-maven-plugin</artifactId>
                <version>1.3.7</version>
                <configuration>
                    <configurationFile>${basedir}/src/main/resources/generator/generatorConfig.xml</configurationFile>
                    <overwrite>true</overwrite>
                    <verbose>true</verbose>
                </configuration>
                <dependencies>
                    <dependency>
                        <groupId>com.github.zsls-lang</groupId>
                        <artifactId>mybatis-expands-generator</artifactId>
                        <version>1.1.0</version>
                    </dependency>
                </dependencies>
            </plugin>
        </plugins>
    </build>


**generatorConfig.xml**

<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration
        PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
        "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">

<generatorConfiguration>

    <context id="Mysql" targetRuntime="MyBatis3Simple" defaultModelType="flat">
        <property name="javaFileEncoding" value="UTF-8"/>


        <plugin type="com.zsls.config.MapperPlugin">
            <property name="mappers" value="com.zsls.base.BaseMapper"/>
            <property name="targetPackage" value="com.zsls.service" />
            <property name="targetProject" value="src/main/java" />
            <property name="baseServiceImpl" value="BaseServiceImpl" />
            <property name="baseServiceImplPackage" value="com.zsls.base.BaseServiceImpl" />

            <property name="baseService" value="IBaseService" />
            <property name="baseServicePackage" value="com.zsls.base.IBaseService" />
            <property name="enableCreateService" value="true" />
            <property name="enableCreateController" value="true" />

            <property name="baseController" value="BaseController" />
            <property name="baseControllerPackage" value="com.zsls.base.BaseController" />
            <property name="controllerTargetPackage" value="com.zsls.controller" />
            <property name="controllerTargetProject" value="src/main/java" />
        </plugin>

        <!-- 这里的type里写的是你的实现类的类全路径 -->
        <commentGenerator type="com.zsls.config.MybatisCommentGenerator" >
            <property name="suppressAllComments" value="false"/>
            <!--<property name="suppressDate" value="true"/>-->
        </commentGenerator>


        <jdbcConnection driverClass="com.mysql.jdbc.Driver"
                        connectionURL="jdbc:mysql://224.16.4.67:3306/data_test?useSSL=false"
                        userId="root"
                        password="password">
        </jdbcConnection>

        <!--<javaModelGenerator targetPackage="com.sunmnet.basedata.model" targetProject="D:\work_new\dx\Data.WEB\basedata\basedata-model\src/main/java"/>-->
        <javaModelGenerator targetPackage="com.zsls.entity" targetProject="src/main/java" >
            <!--<property name="immutable" value="true"/>-->
            <property name="rootClass" value="com.zsls.base.BaseModel"/>
            <property name="trimStrings" value="true" />
            <property name="constructorBased" value="true" />
        </javaModelGenerator>

        <sqlMapGenerator targetPackage="mybatis.statis" targetProject="src/main/resources"/>

        <javaClientGenerator targetPackage="com.zsls.dao" targetProject="src/main/java"
                             type="XMLMAPPER"/>

        <table tableName="analog_data" >
            <!--mysql 配置-->
            <generatedKey column="id" sqlStatement="Mysql" identity="true"/>

        </table>

    </context>
</generatorConfiguration>


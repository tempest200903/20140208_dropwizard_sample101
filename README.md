20140208_dropwizard_sample101
=============================

2014-02-08-133708-Dropwizard入門

  f:/goat-pc-data/ecworkspace/20140208_dropwizard_sample101/README.md
  #+LAST_UPDATED: 2014-02-08

# 2014-02-08-133708-Dropwizard入門 #

## dropwizard-blog-sample を試す ##

https://github.com/spinscale/dropwizard-blog-sample
Dropwizard sample application
This is a small sample application utilizing the nice dropwizard framework, which uses elasticsearch as its storage backend and Mozilla Rhino as javascript rendering engine on the server side (you read that right, no freemarker).

last commit 2 years ago なので古くて動かないかもしれない。

### mvn セットアップ ###

> # mvn --help
> エラー: メイン・クラスorg.codehaus.plexus.classworlds.launcher.Launcherが見つか
> らなかったかロードできませんでした
> # cygpath -w $(which mvn)
> C:\tool\Maven\apache-maven-3.1.1\bin\mvn
> # echo $M2_HOME
> C:\C:\Tools\apache-maven-3.1.1
> # cygpath -u 'C:\tool\Maven\apache-maven-3.1.1'
> /c/tool/Maven/apache-maven-3.1.1
> # export M2_HOME=/c/tool/Maven/apache-maven-3.1.1
> # mvn --version
> Apache Maven 3.1.1 (0728685237757ffbf44136acec0402957f723d9a; 2013-09-18 00:22:2
> 2+0900)
> Maven home: C:\tool\Maven\apache-maven-3.1.1
> Java version: 1.7.0_17, vendor: Oracle Corporation
> Java home: C:\tool\Java\jdk1.7.0_17\jre
> Default locale: ja_JP, platform encoding: MS932
> OS name: "windows 7", version: "6.1", arch: "amd64", family: "windows"

### dropwizard-blog-sample Installation ###

bash
pushd 'F:\goat-pc-data\ecworkspace'
git clone https://github.com/spinscale/dropwizard-blog-sample
mv dropwizard-blog-sample 20140208-dropwizard-blog-sample
cd 20140208-dropwizard-blog-sample
mvn eclipse:eclipse
mvn package
java -jar target/dropwizard-blog-0.0.1-SNAPSHOT.jar
Go to http://localhost:8080/ or to http://localhost:8080/admin with login admin/test123

### mvn package FAILURE ###

> # mvn package
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.710s
> [INFO] Finished at: Sat Feb 08 13:50:57 JST 2014
> [INFO] Final Memory: 21M/309M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed to execute goal org.apache.maven.plugins:maven-surefire-plugin:2.
> 12.4:test (default-test) on project dropwizard-blog: There are test failures.
> [ERROR]
> [ERROR] Please refer to F:\goat-pc-data\ecworkspace\20140208-dropwizard-blog-sam
> ple\target\surefire-reports for the individual test results.
> [ERROR] -> [Help 1]
> 
> # java -jar target/dropwizard-blog-0.0.1-SNAPSHOT.jar
> Error: Unable to access jarfile target/dropwizard-blog-0.0.1-SNAPSHOT.jar

## 自分で dropwizard を組み込んだサンプルを作る ##

http://dev.classmethod.jp/server-side/java/dropwizard/

* cd 'F:\goat-pc-data\ecworkspace'
* mvn archetype:create -DgroupId=com.example -DartifactId=20140208_dropwizard_sample101
* cd 20140208_dropwizard_sample101
* mvn eclipse:eclipse
* Eclipse; Import; Project; F:\goat-pc-data\ecworkspace\20140208_dropwizard_sample101
* F:\goat-pc-data\ecworkspace\20140208_dropwizard_sample101\pom.xml
* mvn eclipse:eclipse

## MavenでdependencyのソースとJavaDocをダウンロードする ##

http://onestopinfolink.wordpress.com/2009/05/17/maven%E3%81%A7dependency%E3%81%AE%E3%82%BD%E3%83%BC%E3%82%B9%E3%81%A8javadoc%E3%82%92%E3%83%80%E3%82%A6%E3%83%B3%E3%83%AD%E3%83%BC%E3%83%89%E3%81%99%E3%82%8B/

> MavenでdependencyのソースとJavaDocをダウンロードする « One Stop Info Link
> maven-eclipse-pluginプラグインを以下のようにPOM内で指定すると、eclipse:eclipseゴールを実行時に自動的にdependencyのソースとJavaDocがダウンロードされます。
> <project>
>   <build>
>     <plugins>
>       <plugin>
>         <artifactId>maven-eclipse-plugin</artifactId>
>         <configuration>
>           <downloadSources>true</downloadSources>
>           <downloadJavadocs>true</downloadJavadocs>
>         </configuration>
>       </plugin>
>     </plugins>
>   </build>
> </project>

* F:\goat-pc-data\ecworkspace\20140208_dropwizard_sample101\pom.xml
    * mvn eclipse:eclipse

## Configurationクラスを作成 ##

F:\goat-pc-data\ecworkspace\20140208_dropwizard_sample101\src\main\java\com\example\HelloWorldConfiguration.java
F:\goat-pc-data\ecworkspace\20140208_dropwizard_sample101\hello-world.yml

## サービスクラスの作成 ##

F:\goat-pc-data\ecworkspace\20140208_dropwizard_sample101\src\main\java\com\example\HelloWorldService.java

## リソースクラスの作成 ##

F:\goat-pc-data\ecworkspace\20140208_dropwizard_sample101\src\main\java\com\example\core\Saying.java
F:\goat-pc-data\ecworkspace\20140208_dropwizard_sample101\src\main\java\com\example\resources\HelloWorldResource.java

## Health Checkクラスの作成 ##

F:\goat-pc-data\ecworkspace\20140208_dropwizard_sample101\src\main\java\com\example\health\TemplateHealthCheck.java

## ビルドと動作確認 ##

> # mvn package
> # java -jar target/20140208_dropwizard_sample101-1.0-SNAPSHOT.jar server hello-world.yml

* http://localhost:8080/hello-world
    * {"id":3,"content":"Hello, Stranger!"}
* http://localhost:8080/hello-world?name=abc
    * {"id":6,"content":"Hello, abc!"}

* F:\goat-pc-data\ecworkspace\20140208_dropwizard_sample101\build.xml に run target を記述した。

## git commit ##

* cd 'F:\goat-pc-data\ecworkspace\github'
* git clone https://github.com/tempest200903/20140208_dropwizard_sample101
* cp -r 'F:\goat-pc-data\ecworkspace\20140208_dropwizard_sample101' .
* cd 20140208_dropwizard_sample101
* git add .
* git commit -m "first commit"
* git push
* pushd 'F:\goat-pc-data\ecworkspace'
* mv 20140208_dropwizard_sample101 20140208_dropwizard_sample101-import
* git clone https://github.com/tempest200903/20140208_dropwizard_sample101

## README ##

F:\goat-pc-data\ecworkspace\20140208_dropwizard_sample101\README.md に本メモを転記する。


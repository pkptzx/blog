---
title: "java校验maven下载的jar文件"
date: 2019-05-23T15:58:08+08:00
draft: false
weight: 70
keywords: ["java","maven"]
description: "description"
tags: ["java","maven"]
categories: ["java"]
author: "码魂"
url: "2019/05/23/java-check-maven-jar"
---
有时候maven真的很坑!

有时候提示invalid LOC header (bad signat signature),

但又有时候什么都不提示,工程报错,情况有肯多中,不知道大家遇到过几种诡异的.

很多人说加-U参数或在maven插件选择强制刷新等操作,但很不好使,一点用都没有.

今天我就遇到POM提示第一行错误,这怎么可能?其他任何地方都不报错,用mvn命令的时候才能看到jar invalid.

我还遇到整个spring的项目只有test报错,其他的都不报错,编辑器里提示的Unknown Error~

真没法玩了~我知道肯定有一个或几个jar下载的有问题.但就算你知道了难道一个一个去找删?一个还好说,有时候5,6个真是浪费时间.

不如就写个代码跑一下吧~

```
public class MvnCheckJar {

  public static void main(String[] args) throws Exception {
      
    String localMvnPath = "F:/mvnlib";
    // 遍历文件夹,找出jar\pom和效验文件进行对比,如果不相符,则删除
    getFile(new File(localMvnPath), "jar,pom");
    System.out.println("完毕");
  }

  public static void getFile(File path, String suffixs) throws Exception {
    String[] suffixs_ = new String[] {};
    if (suffixs != null) suffixs_ = suffixs.split(",");
    if (path.isFile()) {
      for (String suffix : suffixs_) {
        if (path.getName().endsWith(suffix)) {
//            System.out.println(path.getAbsolutePath() ); 
          handler(path);
        }
      }
    } else {
      File[] ff = path.listFiles();
      if(ff!=null)
      for (File x : ff) {
        getFile(x, suffixs);
      }
    }
  }

  /**
   * 验证,发现不匹配则删除
   *
   * @throws IOException
   */
  public static void handler(File f) throws Exception {
    File fsha1 = new File(f.getAbsolutePath() + ".sha1");
    if (fsha1.exists()) {
      String sha1 =
          FileUtils.readFileToString(fsha1, "utf-8").replaceAll("(?m).*(\\w{40}).*", "$1").replaceAll("\\n|\\r", "");
      String currsha1 = sha1(f);
      if(!sha1.equals(currsha1)){//如果不等,则删除 当前文件和sha1
//          System.out.println("sha1file: " + sha1 ); 
          fsha1.delete();
          f.delete();
      System.out.println(sha1 + " , " + currsha1 + " , " + f.getAbsolutePath());
      
      }

    } else {
      f.delete();
    }
  }

  public static String sha1(File f) throws Exception {
    try (FileInputStream fis = new FileInputStream(f)) {
      return org.apache.commons.codec.digest.DigestUtils.sha1Hex(fis);
    }
  }
}
```
---
title: "使用java将SVG图片格式转PNG图片格式"
date: 2021-03-19T15:29:12+08:00
draft: false
weight: 70
keywords: ["svg","png","图片","转换"]
description: "将SVG图片格式转换为PNG图片"
tags: ["java","image"]
categories: ["java"]
author: "码魂"
url: "2021/03/19/svg-convert-png"
---

```xml
<dependency>
    <groupId>org.apache.xmlgraphics</groupId>
    <artifactId>xmlgraphics-commons</artifactId>
    <version>2.6</version>
</dependency>
<dependency>
    <groupId>org.apache.xmlgraphics</groupId>
    <artifactId>batik-all</artifactId>
    <version>1.14</version>
    <type>pom</type>
</dependency>
```

```java
import java.io.ByteArrayInputStream;
import java.io.File;
import java.io.FileOutputStream;
import java.io.FilenameFilter;
import java.io.OutputStream;

import org.apache.batik.transcoder.TranscoderInput;
import org.apache.batik.transcoder.TranscoderOutput;
import org.apache.batik.transcoder.image.PNGTranscoder;
import org.apache.commons.io.FileUtils;

public class SVG2PNG {
  /**
   * 将指定目录中的svg文件转换成png格式
   * 
   * @param args
   * @throws Exception
   */
  public static void main(String[] args) throws Exception {
    File[] svgs = new File("H:\\tmp\\图标").listFiles(new FilenameFilter() {
      @Override
      public boolean accept(File dir, String name) {
        return name.endsWith("svg");
      }
    });
    for (File file : svgs) {
      convertToPng(file);
    }
  }

  public static boolean convertToPng(File svgFile) throws Exception {

    OutputStream outputStream = null;
    try {
      String pngName = svgFile.getName().replaceAll("svg$", "png");
      outputStream = new FileOutputStream(svgFile.getParent() + "\\" + pngName);

      byte[] svg = FileUtils.readFileToByteArray(svgFile);

      PNGTranscoder t = new PNGTranscoder();

      TranscoderInput input = new TranscoderInput(new ByteArrayInputStream(svg));

      TranscoderOutput output = new TranscoderOutput(outputStream);

      t.transcode(input, output);

    } catch (Exception e) {
      e.printStackTrace();
      return false;
    } finally {
      if (outputStream != null) {
        outputStream.close();
      }
    }
    return true;
  }
}
```

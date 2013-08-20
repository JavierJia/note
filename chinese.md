# some dicts
https://code.google.com/p/vimim-data/wiki/Download

# UTF8 and unicode mapping:
http://www.utf8-chartable.de/unicode-utf8-table.pl

#GB18030:
http://baike.baidu.com/view/889058.htm
高位0x81~0xFE
低位0x40~0x7E  &  0x80~0xFE

#GB2312
汉字区的“高位字节”的范围是0xB0-0xF7，“低位字节”的范围是0xA1-0xFE

All characters :
http://www.knowsky.com/resource/gb2312tbl.htm

# GBK
http://zh.wikipedia.org/wiki/GBK

# CJK
http://zh.wikipedia.org/wiki/%E4%B8%AD%E6%97%A5%E9%9F%93%E7%B5%B1%E4%B8%80%E8%A1%A8%E6%84%8F%E6%96%87%E5%AD%97

# CharSet and Encoding:
http://www.cnblogs.com/skynet/archive/2011/05/03/2035105.html

# The way of Lucene deal with CharType
http://grepcode.com/file/repo1.maven.org/maven2/org.apache.lucene/lucene-analyzers-smartcn/4.3.1/org/apache/lucene/analysis/cn/smart/Utility.java#Utility.getCharType%28char%29
```Java
public static int More ...getCharType(char ch) {
        // Most (but not all!) of these are Han Ideographic Characters
        if (ch >= 0x4E00 && ch <= 0x9FA5)
          return CharType.HANZI;
        // A || a
        if ((ch >= 0x0041 && ch <= 0x005A) || (ch >= 0x0061 && ch <= 0x007A))
          return CharType.LETTER;
        if (ch >= 0x0030 && ch <= 0x0039)
          return CharType.DIGIT;
        if (ch == ' ' || ch == '\t' || ch == '\r' || ch == '\n' || ch == '　')
          return CharType.SPACE_LIKE;
        // Punctuation Marks
        if ((ch >= 0x0021 && ch <= 0x00BB) || (ch >= 0x2010 && ch <= 0x2642)
            || (ch >= 0x3001 && ch <= 0x301E))
          return CharType.DELIMITER;
    
        // Full-Width range
        // Ａ|| ａ 
        if ((ch >= 0xFF21 && ch <= 0xFF3A) || (ch >= 0xFF41 && ch <= 0xFF5A))
          return CharType.FULLWIDTH_LETTER;
        // ０
        if (ch >= 0xFF10 && ch <= 0xFF19)
          return CharType.FULLWIDTH_DIGIT;
        if (ch >= 0xFE30 && ch <= 0xFF63)
          return CharType.DELIMITER;
        return CharType.OTHER;
    
      }
```

---
layout: post
title:  "Python —— Python中pytesseract库的使用以及注意事项"
date:   2020-08-06 22:46:13
categories: Python
permalink: /archivers/how-to-use-pytesseract
---

> 当我们在使用pytesseract库的时候，使用 pip install pytesseract安装完成后，发现它并不能识别出图片内容，并且会抛出异常pytesseract.pytesseract.TesseractNotFoundError: tesseract is not installed or it's not in your PATH. See README file for more information.
> 这是怎么回事呢？今天让我们一探究竟

### 1. 尝试

使用代码

```python
import pytesseract
from PIL import Image

image = Image.open("./NormalImg.png")
text = pytesseract.image_to_string(image)
print(text)
```

报错提示：

```shell
    raise TesseractNotFoundError()
pytesseract.pytesseract.TesseractNotFoundError: tesseract is not installed or it's not in your PATH. See README file for more information.
```

### 2. 官方文档

pytesseract官方文档：https://pypi.org/project/pytesseract/

是我们缺少了[tesseract](https://github.com/UB-Mannheim/tesseract)程序

tesseract官方Github地址：https://github.com/UB-Mannheim/tesseract

tesseract官方Github说明https://github.com/UB-Mannheim/tesseract/wiki

### 3. 安装tesseract

下载地址

Tesseract 5.0.0 32位版本：[tesseract-ocr-w32-setup-v5.0.0-alpha.20200328.exe](https://digi.bib.uni-mannheim.de/tesseract/tesseract-ocr-w32-setup-v5.0.0-alpha.20200328.exe) (32 bit) 

Tesseract 5.0.0 64位版本：[tesseract-ocr-w64-setup-v5.0.0-alpha.20200328.exe](https://digi.bib.uni-mannheim.de/tesseract/tesseract-ocr-w64-setup-v5.0.0-alpha.20200328.exe) (64 bit) 

### 4. 导入tesseract.exe执行文件地址

添加以下导入路径：

```python
pytesseract.pytesseract.tesseract_cmd = r'C:\Program Files\Tesseract-OCR\tesseract.exe'
```

最终代码：

```python
import pytesseract
from PIL import Image

pytesseract.pytesseract.tesseract_cmd = r'C:\Program Files\Tesseract-OCR\tesseract.exe'
image = Image.open("./NormalImg.png")
text = pytesseract.image_to_string(image)
print(text)
```

至此运行代码不会异常，并可以正常读取图片文字内容

### 5. 总结

pytesseract包依赖于Tesseract执行文件，需要安装Tesseract

当然Tesseract只能识别标准的ASCII字符串，复杂的验证吗就无法使用pytesseract来读取了



*****



欢迎来跟博主讨论Python有关的问题。
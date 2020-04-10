#!/usr/bin/python

from PIL import Image

#底图命名为picture1,表图命名为picture2

w=int(input("请输入结果图片宽度:"))
h=int(input("请输入结果图片高度:"))


print("准备处理picture1")
img1 = Image.open("picture1.png")
img1 = img1.convert("L")
img1 = img1.convert('RGBA')
img1 = img1.resize((w,h))

maxImg1i, maxImg1j = img1.size
img1i = -1
img1j = -1

print("正在处理picture1..")
while (img1i < maxImg1i - 1):
    img1i += 1
    img1j = -1
    while (img1j < maxImg1j - 1):
        img1j += 1

        img1num1, img1num2, img1num2, img1num2 = img1.getpixel((img1i, img1j))
        img1.putpixel((img1i, img1j), (255, 255, 255, img1num1))

        if (img1i % 2 != 0):
            if (img1j % 2 != 0):
                img1.putpixel((img1i, img1j), (0, 0, 0, 0))
        else:
            if (img1j % 2 == 0):
                img1.putpixel((img1i, img1j), (0, 0, 0, 0))

print("picture1处理完毕")
print("***")


print("准备处理picture2")
img2 = Image.open("picture2.png")
img2 = img2.convert("L")
img2 = img2.convert('RGBA')
img2 = img2.resize((w,h))

maxImg2i, maxImg2j = img2.size
img2i = -1
img2j = -1

print("正在处理picture2..")
while (img2i < maxImg2i - 1):
    img2i += 1
    img2j = -1
    while (img2j < maxImg2j - 1):
        img2j += 1

        img1num3, img1num4, img1num4, img1num4 = img2.getpixel((img2i, img2j))
        img2.putpixel((img2i, img2j), (0, 0, 0, 255 - img1num3))

        if (img2i % 2 != 1):
            if (img2j % 2 != 0):
                img2.putpixel((img2i, img2j), (0, 0, 0, 0))
        else:
            if (img2j % 2 == 0):
                img2.putpixel((img2i, img2j), (0, 0, 0, 0))

print("picture2处理完毕")
print("***")


print("开始合并图片")

img1i=-1
img1j=-1

while (img1i < maxImg1i - 1):
    img1i += 1
    img1j = -1
    while (img1j < maxImg1j - 1):
        img1j += 1

        if (img1i % 2 != 0):
            if (img1j % 2 != 0):
                img1.putpixel((img1i, img1j), img2.getpixel((img1i, img1j)))
        else:
            if (img1j % 2 == 0):
                img1.putpixel((img1i, img1j), img2.getpixel((img1i, img1j)))

print("合并完毕")

img1.save("tank.png")

print("已保存至“tank.png”")

input()

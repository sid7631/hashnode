---
title: "How to create QR Code Generator"
seoTitle: "HashNode - How to create QR Code Generator"
datePublished: Thu Jun 22 2023 16:25:53 GMT+0000 (Coordinated Universal Time)
cuid: clj7cuj7x00000al8e7mf693h
slug: create-qr-code-generator
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1687450612394/2ebe3950-aee3-446f-a87a-5ccb70491588.png
tags: qr-code, qr-code-generator, react-qr

---

## **I**ntroduction

Welcome to this tutorial on how to create a QR code generator website. QR Codes, or Quick Response codes, are becoming increasingly popular as a means of sharing information quickly and easily. In this tutorial, we’ll walk you through the process of creating a website that generates QR codes for any text or URL you enter.

## Requirements

* HTML, CSS, JavaScript
    
* Code Editor / VS Code
    

To get started, we need to create the basic structure of our website using HTML and style it using CSS.

## Getting Started

### *index.html*

```xml
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>QR Code Generator</title>
    <link rel="stylesheet" href="app.css" />
</head>
<body>
        <main class="container bg-white">
            <section class="heading">
                <div class="title">QR Codes</div>
                <div class="sub-title">Create Custom QR Codes for your brand</div>
            </section>
            <section class="user-input">
                <input type="text" name="search" id="qr-text" placeholder="Generate QR for anything...">
                <button id="generate-qr">Generate</button>
            </section>
            <div class="qr-container">
                <div class="qr-code"></div>
            </div>
        </main>
</body>
</html>
```

### *app.css*

```css
.bg-white {
    background-color: rgb(255 255 255 / 1);
}

.container {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    padding-top: 12rem;
}

.heading {
    text-align: center;
}

.title {
    font-size: 3.75rem;
    letter-spacing: -0.025em;
}

.sub-title {
    font-size: 1.125rem;
    line-height: 2rem;
    color: rgb(75 85 99 / 1);
    margin-top: 0.5rem;
}

.user-input {
    margin-top: 2.5rem;
}

.qr-container {
    padding: 2rem;
}

.qr-code {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
}

.qr-code img {
    padding: 1rem;
    border:2px solid black;
    margin-bottom: 1.5rem;
    border-radius: 5px;
}

.qr-code button a {
    text-decoration: none;
    color: black;
}
```

Here’s what our code looks like.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687449254920/53cd414b-c0a3-4db5-a8de-714645533ed7.png align="center")

Now that we have our basic website structure in place, we need to add the functionality to generate QR codes. We’ll be using a Javascript library called qrcodes.js to do this. Here’s the code we need to add to our HTML file to include the library.

```xml
<script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>h
```

Next, we need to add the code that will generate the QR code based on the user input. Here’s what that looks like

Add to index.html

```xml
<script src="app.js"> </script>
```

### app.js

```javascript
let btn = document.getElementById('generate-qr')
let qr_code_element = document.querySelector(".qr-code")

btn.addEventListener("click", () => {
    let user_input = document.querySelector('#qr-text')
    if(user_input.value != "") {
        if(qr_code_element.childElementCount==0){
            generate_qr(user_input)
        } else {
            qr_code_element.innerHTML = ''
            generate_qr(user_input)
        }
    } else {
        console.log("not valid")
        qr_code_element.style = "display:none"
    }
})

function generate_qr(user_input) {
    qr_code_element.style = ''
    var qrcode = new QRCode(document.querySelector(".qr-code"), {
        text: `${user_input.value}`,
        width: 180, //default 128
        height: 180,
        colorDark : "black",
        colorLight : "#ffffff",
        correctLevel : QRCode.CorrectLevel.H
    });
}
```

Now we have our QR code generator up and running! But we can make it even better by allowing users to download the QR code as an image file. Here’s the Javascript code we need to add to our app.js file to do that.

```javascript
let download = document.createElement("button")
qr_code_element.appendChild(download);

let download_link = document.createElement("a");
download_link.setAttribute("download", "qr_code.png");
download_link.innerHTML = `Download <i class="fa-solid fa-download"></i>`;

download.appendChild(download_link);
let qr_code_img = document.querySelector(".qr-code img");
let qr_code_canvas = document.querySelector("canvas");

if (qr_code_img.getAttribute("src") == null) {
    setTimeout(() => {
        download_link.setAttribute("href", `${qr_code_canvas.toDataURL()}`);
    }, 300);
} else {
    setTimeout(() => {
        download_link.setAttribute("href", `${qr_code_img.getAttribute("src")}`);
    }, 300);
}
```

And that’s it! We’ve created a simple yet effective QR code generator website using HTML, CSS and JavaScript.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687449440122/aecd2862-2c44-4a42-a617-62966fce47f8.png align="center")

With a little more time and effort, you could add additional features like the ability to change the colour or size of the QR code.

Thanks

## GitHub repository

%[https://github.com/sid7631/qr-code-generator]
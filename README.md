[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/UQL1B0Jv)

## Progress :
1. Membuat tulisan 3 huruf awal menggunakan 

## Chat Gpt:

![Pertanyaan 1](/Gambar/Q1.jpeg)
![Jawaban 1](/Gambar/A1.jpeg)

## Penjelasan Code:

```
// Step 1: Set up the canvas
        const canvas = document.getElementById('glCanvas');

        // Step 2: Initialize WebGL context
        const gl = canvas.getContext('webgl');
```
Pertama buat canvas dan ambil element dari html yang memiliki id glCanvas, setelah inisialisai konteks webgl
```
        // Step 3: Compile shaders
        const vertexShaderSource = `
            // Vertex shader code (GLSL)
            attribute vec2 a_position;
            attribute vec3 a_color;
            varying vec3 v_color;

            void main() {
                // Set the position of the vertex
                gl_Position = vec4(a_position, 0.0, 1.0);
                v_color = a_color;
            }
        `;
        const fragmentShaderSource = `
            // Fragment shader code (GLSL)
            precision mediump float;
            varying vec3 v_color;
            void main() {
                gl_FragColor = vec4(v_color, 1.0);
            }
        `;
```
Selanjutnya saya memperbarui kode fragment shader dan mengirimkan warna yang berbeda sebagai atribut ke dalam vertex shader. Dengan a_color adalah atribut warna dan v-color adalah variabel untuk mengirim warna ke fragment shader.
Lalu pada fragment shader v_color menerima warna dari vertex shader menggunakan varying.

```
const vertexShader = gl.createShader(gl.VERTEX_SHADER);
        gl.shaderSource(vertexShader, vertexShaderSource);
        gl.compileShader(vertexShader);

        const fragmentShader = gl.createShader(gl.FRAGMENT_SHADER);
        gl.shaderSource(fragmentShader, fragmentShaderSource);
        gl.compileShader(fragmentShader);
```

```
// Step 4: Create and link program
        const program = gl.createProgram();
        gl.attachShader(program, vertexShader);
        gl.attachShader(program, fragmentShader);
        gl.linkProgram(program);
        gl.useProgram(program);
```
Selanjutnya buat dan link program.

```
// Step 5: Set up attributes and uniforms
        const positionAttributeLocation =  gl.getAttribLocation(program, 'a_position')
        const positionBuffer = gl.createBuffer();
```
Selanjutnya set up atribut dan uniform.

Lalu kode dibawah adalah vector untuk membentuk nama saya.
Pada vektor tersebut dibagi menjadi 2 zona yaitu lines dan triangle, jadi saya menggabung vektor untuk line dan vektor untuk segitiga dalah satu array.
Lalu array akan dibaca setiap 5 baris, dimana 2 baris pertama adalah koordinat x, y dan 3 baris berikutnya adalah warna untuk fragment tersebut.
```
const positionData = new Float32Array([
            ///Lines
        ////R
            //1
        -0.6, 0.5, 0.612, 0.965, 0.965, 
        -0.6, -0.4, 0.612, 0.965, 0.965, 
        -0.55, 0.5, 0.612, 0.965, 0.965, 
        -0.55, -0.4, 0.612, 0.965, 0.965, 
            //2
        -0.55, 0.5, 0.612, 0.965, 0.965, 
        -0.25, 0.5, 0.612, 0.965, 0.965, 
        -0.55, 0.4, 0.612, 0.965, 0.965, 
        -0.25, 0.4, 0.612, 0.965, 0.965, 
            //3
        -0.3, 0.4, 0.612, 0.965, 0.965, 
        -0.3, 0, 0.612, 0.965, 0.965, 
        -0.25, 0.4, 0.612, 0.965, 0.965, 
        -0.25, 0, 0.612, 0.965, 0.965, 
            //4
        -0.3, 0.1, 0.612, 0.965, 0.965, 
        -0.55, 0.1, 0.612, 0.965, 0.965, 
        -0.3, 0, 0.612, 0.965, 0.965, 
        -0.55, 0, 0.612, 0.965, 0.965, 
            //5
        -0.4, 0, 0.612, 0.965, 0.965, 
        -0.37, -0.4, 0.612, 0.965, 0.965, 
        -0.42, -0.4, 0.612, 0.965, 0.965, 
        -0.45, 0, 0.612, 0.965, 0.965, 
        
        
        ////A
            //1
        -0.6 + 0.5, 0.5, 0.612, 0.965, 0.965, 
        -0.6 + 0.5, -0.4, 0.612, 0.965, 0.965, 
        -0.55 + 0.5, 0.5, 0.612, 0.965, 0.965, 
        -0.55 + 0.5, -0.4, 0.612, 0.965, 0.965, 
            //2
        -0.55 + 0.5, 0.5, 0.612, 0.965, 0.965, 
        -0.25 + 0.5, 0.5, 0.612, 0.965, 0.965, 
        -0.55 + 0.5, 0.4, 0.612, 0.965, 0.965, 
        -0.25 + 0.5, 0.4, 0.612, 0.965, 0.965, 
            //3
        -0.3 + 0.5, 0.4, 0.612, 0.965, 0.965, 
        -0.3 + 0.5, -0.4, 0.612, 0.965, 0.965, 
        -0.25 + 0.5, 0.4, 0.612, 0.965, 0.965, 
        -0.25 + 0.5, -0.4, 0.612, 0.965, 0.965, 
            //4
        -0.3 + 0.5, 0.1, 0.612, 0.965, 0.965, 
        -0.55 + 0.5, 0.1, 0.612, 0.965, 0.965, 
        -0.3 + 0.5, 0, 0.612, 0.965, 0.965, 
        -0.55 + 0.5, 0, 0.612, 0.965, 0.965, 

        ////F
            //1
        -0.6 + 0.5 + 0.5, 0.5, 0.612, 0.965, 0.965, 
        -0.6 + 0.5 + 0.5, -0.4, 0.612, 0.965, 0.965, 
        -0.55 + 0.5 + 0.5, 0.5, 0.612, 0.965, 0.965, 
        -0.55 + 0.5 + 0.5, -0.4, 0.612, 0.965, 0.965, 
            //2
        -0.55 + 0.5 + 0.5, 0.5, 0.612, 0.965, 0.965,
        -0.25 + 0.5 + 0.5, 0.5, 0.612, 0.965, 0.965, 
        -0.55 + 0.5 + 0.5, 0.4, 0.612, 0.965, 0.965,
        -0.25 + 0.5 + 0.5, 0.4, 0.612, 0.965, 0.965, 
            //3
        -0.3 + 0.5 + 0.5, 0.1, 0.612, 0.965, 0.965, 
        -0.55 + 0.5 + 0.5, 0.1, 0.612, 0.965, 0.965, 
        -0.3 + 0.5 + 0.5, 0, 0.612, 0.965, 0.965, 
        -0.55 + 0.5 + 0.5, 0, 0.612, 0.965, 0.965,             


            ///Triangle
        ///////R
            -0.1 - 0.42, 0 -0.25,  0.0, 0.0, 0.0, 
            -0.1 - 0.42, 0.7 -0.25,   0.0, 0.0, 0.0,  
            -0.05 - 0.42,  0 -0.25,     0.0, 0.0, 0.0, 

            -0.1 - 0.42, 0.7 -0.25,    0.0, 0.0, 0.0, 
            0.15 - 0.42, 0.7 -0.25,    0.0, 0.0, 0.0, 
            -0.1 - 0.42,  0.65 -0.25,  0.0, 0.0, 0.0, 

            0.15 - 0.42, 0.7 -0.25,  0.0, 0.0, 0.0,
            0.13 - 0.42, 0.7 -0.25,  0.0, 0.0, 0.0, 
            0.15 - 0.42, 0.35 -0.25,  0.0, 0.0, 0.0, 

            0.15 - 0.42, 0.35 -0.25,  0.0, 0.0, 0.0, 
            0.15 - 0.42, 0.39 -0.25,  0.0, 0.0, 0.0, 
            -0.1 - 0.42, 0.35 -0.25,  0.0, 0.0, 0.0, 

            -0.1 - 0.42, 0.38 -0.25,  0.0, 0.0, 0.0, 
            0.15 - 0.42, 0 -0.25,  0.0, 0.0, 0.0, 
            0.15 - 0.42, 0.05 -0.25,  0.0, 0.0, 0.0, 

        ////////A

            -0.1 + 0.4 - 0.35, 0 -0.25,    0.0, 0.0, 0.0, 
            -0.1 + 0.4 - 0.35, 0.7 -0.25,    0.0, 0.0, 0.0, 
            -0.05 + 0.4 - 0.35,  0 -0.25,     0.0, 0.0, 0.0, 

            -0.1 + 0.4 - 0.35, 0.7 -0.25,    0.0, 0.0, 0.0, 
            0.15 + 0.4 - 0.35, 0.7 -0.25,    0.0, 0.0, 0.0, 
            -0.1 + 0.4 - 0.35,  0.65 -0.25,  0.0, 0.0, 0.0, 

            0.15 + 0.4 - 0.35, 0.7 -0.25,  0.0, 0.0, 0.0, 
            0.13 + 0.4 - 0.35, 0.7 -0.25,  0.0, 0.0, 0.0, 
            0.15 + 0.4 - 0.35, 0.35 -0.25,  0.0, 0.0, 0.0, 

            0.15 + 0.4 - 0.35, 0.35 -0.25,  0.0, 0.0, 0.0, 
            0.15 + 0.4 - 0.35, 0.39 -0.25,  0.0, 0.0, 0.0, 
            -0.1 + 0.4 - 0.35, 0.35 -0.25,  0.0, 0.0, 0.0, 

            0.1 + 0.4 - 0.35, 0 -0.25,  0.0, 0.0, 0.0, 
            0.15 + 0.4 - 0.35, 0 -0.25,  0.0, 0.0, 0.0, 
            0.15 + 0.4 - 0.35, 0.7 -0.25,  0.0, 0.0, 0.0, 


            /////////F
            -0.1 + 0.8 - 0.3, 0 -0.25,    0.0, 0.0, 0.0, 
            -0.1 + 0.8 - 0.3, 0.7 -0.25,    0.0, 0.0, 0.0, 
            -0.05 + 0.8 - 0.3,  0 -0.25,     0.0, 0.0, 0.0, 

            -0.1 + 0.8 - 0.3, 0.7 -0.25,   0.0, 0.0, 0.0, 
            0.15 + 0.8 - 0.3, 0.7 -0.25,    0.0, 0.0, 0.0, 
            -0.1 + 0.8 - 0.3,  0.65 -0.25,  0.0, 0.0, 0.0, 

            0.15 + 0.8 - 0.3, 0.35 -0.25,  0.0, 0.0, 0.0, 
            0.15 + 0.8 - 0.3, 0.39 -0.25,  0.0, 0.0, 0.0, 
            -0.1 + 0.8 - 0.3, 0.35 -0.25,  0.0, 0.0, 0.0, 

        ])
        const colorAttributeLocation = gl.getAttribLocation(program, 'a_color');
        const colorBuffer = gl.createBuffer();
        ```

    
    ```
    // Step 6: Create and bind buffers
        gl.bindBuffer(gl.ARRAY_BUFFER, positionBuffer);
        gl.bufferData(gl.ARRAY_BUFFER, positionData, gl.STATIC_DRAW);
        gl.enableVertexAttribArray(positionAttributeLocation);
        gl.vertexAttribPointer(positionAttributeLocation, 2, gl.FLOAT, false, 20, 0);

        gl.bindBuffer(gl.ARRAY_BUFFER, colorBuffer);
        gl.bufferData(gl.ARRAY_BUFFER, positionData, gl.STATIC_DRAW);
        gl.enableVertexAttribArray(colorAttributeLocation);
        gl.vertexAttribPointer(colorAttributeLocation, 3, gl.FLOAT, false, 20, 8);
    ```

    Kode dibawah adalah kode untuk render, dimana saya membuat 2 fungsi render yang masing masing untuk merender lines dan triangle.
    
    ```
    // Step 7: Rendering loop
        function render() {
            gl.clearColor(0.0, 0.0, 0.0, 1.0);

            // Clear canvas
            gl.clear(gl.COLOR_BUFFER_BIT);

            // Draw the triangle using gl.drawArrays
            gl.drawArrays(gl.LINE_LOOP, 0, 2);
            gl.drawArrays(gl.LINE_LOOP, 2, 2);
            gl.drawArrays(gl.LINE_LOOP, 4, 2);
            gl.drawArrays(gl.LINE_LOOP, 6, 2);
            gl.drawArrays(gl.LINE_LOOP, 8, 2);
            gl.drawArrays(gl.LINE_LOOP, 10, 2);
            gl.drawArrays(gl.LINE_LOOP, 12, 2);
            gl.drawArrays(gl.LINE_LOOP, 14, 2);
            gl.drawArrays(gl.LINE_LOOP, 16, 2);
            gl.drawArrays(gl.LINE_LOOP, 18, 2);
            gl.drawArrays(gl.LINE_LOOP, 20, 2);

            gl.drawArrays(gl.LINE_LOOP, 22, 2);
            gl.drawArrays(gl.LINE_LOOP, 24, 2);
            gl.drawArrays(gl.LINE_LOOP, 26, 2);
            gl.drawArrays(gl.LINE_LOOP, 28, 2);
            gl.drawArrays(gl.LINE_LOOP, 30, 2);
            gl.drawArrays(gl.LINE_LOOP, 32, 2);
            gl.drawArrays(gl.LINE_LOOP, 34, 2);

            gl.drawArrays(gl.LINE_LOOP, 36, 2);
            gl.drawArrays(gl.LINE_LOOP, 38, 2);
            gl.drawArrays(gl.LINE_LOOP, 40, 2);
            gl.drawArrays(gl.LINE_LOOP, 42, 2);
            gl.drawArrays(gl.LINE_LOOP, 44, 2);
            gl.drawArrays(gl.LINE_LOOP, 46, 2);

            requestAnimationFrame(render);
        }
    ```
    Fungsi render() : pada fungsi ini saya mengubah warna background menjadi hitam menggunakan gl.clearcolor, lalu saya mulai menggambar menggunakan draw arrays mulai dari array 1 sampai array 47 dengan setiap gambar diambil 2 array jadi kelipatan 2. 
    ```
    function render2(){
            gl.clearColor(0.612, 0.965, 0.965, 1.0);
            gl.clear(gl.COLOR_BUFFER_BIT);

            gl.drawArrays(gl.TRIANGLES, 48, 3);
            gl.drawArrays(gl.TRIANGLES, 51, 3);
            gl.drawArrays(gl.TRIANGLES, 54, 3);
            gl.drawArrays(gl.TRIANGLES, 57, 3);
            gl.drawArrays(gl.TRIANGLES, 60, 3);


            gl.drawArrays(gl.TRIANGLES, 63, 3);
            gl.drawArrays(gl.TRIANGLES, 66, 3);
            gl.drawArrays(gl.TRIANGLES, 69, 3);
            gl.drawArrays(gl.TRIANGLES, 72, 3);
            gl.drawArrays(gl.TRIANGLES, 75, 3);


            gl.drawArrays(gl.TRIANGLES, 78, 3);
            gl.drawArrays(gl.TRIANGLES, 81, 3);
            gl.drawArrays(gl.TRIANGLES, 84, 3);

            requestAnimationFrame(render2);
        }
    ```
    Fungsi render2() : pada fungsi ini saya mengubah warna background menjadi skyblue menggunakan gl.clearcolor, lalu saya mulai menggambar menggunakan draw arrays mulai dari array 48 sampai array 86 dengan setiap gambar diambil 3 array jadi kelipatan 3. 

    Setelah itu untuk melakukan render 2 fungsi tadi secara bergantian saya menggunakan setInterval dengan interval 3 detik, dimana yang di interval kan adalah fungsi switchWebGLCode.
    Pada fungsi tersebut akan ada variabel currentCode yang berfungsi seperti boolean, lalu setiap loop pada setInterval variabel tersebut akan ditukar2 agar fungsi render yang berjalan bergantian.
    ```
    let currentCode = 1; // Start with WebGL Code 1

        function switchWebGLCode() {
            if (currentCode === 1) {
                render2();
            } else {
                render();
            }

            currentCode = (currentCode === 1) ? 2 : 1; // Toggle between 1 and 2
        }

        setInterval(switchWebGLCode,3000);
    ```
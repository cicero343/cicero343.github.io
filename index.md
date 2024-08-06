---
Title: A Diary of IT Projects
---
<img src="https://avatars.githubusercontent.com/u/175522457?v=4" width="125" height="125" style="border-radius: 20px;">

html {
    color-scheme: light dark;
}

html {
    --bg-color: #ffffff;
    --txt-color: #000000;
}

@supports (background-color: Canvas) and (color: CanvasText) {
    :root {
        --bg-color: Canvas;
        --txt-color: CanvasText;
    }
}

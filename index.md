---
Title: A Diary of IT Projects
---
<img src="https://avatars.githubusercontent.com/u/175522457?v=4" width="125" height="125" style="border-radius: 20px;">

<span style="background-color: #004aad;">highlighted text.</span>

<span style="background-image: url('https://i0.wp.com/www.learnically.com/wp-content/uploads/2023/05/html-strucher.jpg'); background-size: cover; font-size: 20pt; color: white; padding: 10px;">
  Learnically presents...
</span>

.scrolling-text {
  white-space: nowrap;
  overflow: hidden;
  box-sizing: border-box;
  display: inline-block;
  padding-left: 100%;
  animation: marquee 10s linear infinite;
}

@keyframes marquee {
  0% {
    transform: translateX(100%);
  }
  100% {
    transform: translateX(-100%);
  }
}

<script>
  var text = "";
  var author = "";
  var typed = "";
  var progress = 0;
  var inputdisabled = false;
  var bgcolor = "";

  var typing = false;

  var time = 0;

  refresh();

  setInterval(() => {
    if (typing == true) {
      time += 0.1;
    }
  }, 100);

  function type() {
    if (typing == false) {
      typing = true;
    }
    // Checks if typed charcters are correct
    bgcolor = "background-color: #fff";
    if (typed.slice(0, typed.length) == text.slice(0, typed.length)) {
      console.log("String is correct!");

      progress = (typed.length / text.length) * 100;

      // Check if the quote has been completed
      if (typed.length == text.length && typed == text) {
        console.log("String typed successfully!");
        typing = false;
        inputdisabled = true;
        typed = `${math.round(time, 1)}s | ${math.round(
          text.length / 5 / (time / 60),
          1
        )} WPM | Quote from ${author}`;
        bgcolor = "background-color: #ccffe6";
      }
    } else {
      console.log("There's been a typing mistake...");
      bgcolor = "background-color: #ffcccc";
    }
  }

  function refresh() {
    fetch("https://api.quotable.io/random")
      .then((response) => response.json())
      .then((data) => {
        console.log(`${data.content} —${data.author}`);
        text = data.content;
        author = data.author;
      });
  }

  function restart() {
    time = 0;
    progress = 0;
    typed = "";
    inputdisabled = false;
    typing = false;
    bgcolor = "#fff";
    refresh();
  }
</script>

<svelte:head>
  <script
    src="https://kit.fontawesome.com/347d7d5619.js"
    crossorigin="anonymous"></script>
  <script
    src="https://cdnjs.cloudflare.com/ajax/libs/mathjs/9.2.0/math.js"
    integrity="sha512-SewEag0kt1xsJdbfAXgLyLvYXeAoGEla4M6JSitT6ocJVI+VeUbFXkgrbloNn4cVgq46caRf31un2eoalq6YOw=="
    crossorigin="anonymous"></script>
</svelte:head>

<body style={bgcolor}>
  <div />
  <div>
    <h1 class="title">Haste</h1>
    <div class="textbox">
      <p>{text}</p>
    </div>
    <div class="progressbar-outer">
      <div class="progressbar-inner" style="width: {progress}%" />
    </div>
    <div class="typebox-container">
      <input
        class="typebox"
        disabled={inputdisabled}
        placeholder="Type here!"
        type="text"
        onselectstart="return false"
        onpaste="return false;"
        onCopy="return false"
        onCut="return false"
        onDrag="return false"
        onDrop="return false"
        autocomplete="off"
        bind:value={typed}
        on:input={type}
      />
    </div>
    <div class="restartdiv">
      <button class="restart" on:click={restart}>
        <i class="fas fa-repeat-alt fa-lg" />
      </button>
    </div>
  </div>

  <div class="footer">
    <span class="footer-right">
      <a href="https://github.com/gradientmz">Github</a>
      <a href="https://twitter.com/gradientapps">Twitter</a>
      <a href="https://github.com/gradientmz/haste">Repo</a>
    </span>
  </div>
</body>

<style>
  @font-face {
  font-family: Inter;
  src: url(inter.ttf);
  }

  body {
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: "Inter", sans-serif;
    color: #171f36;
    transition: 0.25s;
  }
  .title {
    font-size: 3rem;
    margin: 0rem;
    text-align: center;
  }
  p {
    text-align: center;
    font-size: 1.25rem;
    margin-left: 1rem;
    margin-right: 1rem;
  }
  .typebox-container {
    text-align: center;
  }
  .typebox {
    font-size: 1.25rem;
    padding: 1rem 1rem;
    border: 1px solid gray;
    width: 60vw;
    border: 2px solid lightgray;
    border-radius: 0.5rem;
    background-color: whitesmoke;
    margin: auto;
  }
  .restartdiv {
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .restart {
    font-size: 1.5rem;
    margin-top: 1.25rem;
    border: 2px solid lightgray;
    border-radius: 0.5rem;
    padding: 0.5rem 1rem;
  }
  .restart:focus {
    border-color: black;
  }
  .progressbar-outer {
    height: 0.75rem;
    width: 60vw;
    margin: auto;
    margin-bottom: 1.25rem;
    border-radius: 0.5rem;
    background-color: #ebebeb;
  }
  .progressbar-inner {
    height: 0.75rem;
    border-radius: 0.5rem;
    background-color: #ffe100;
    transition: 0.2s;
  }
  .footer {
    background: #151927;
    font-family: arial;
    padding: 10px;
    bottom: 0;
    position: fixed;
    width: 100%;
    left: -5px;
    text-align: center;
  }
  .footer:after {
    display: block;
    clear: both;
    content: "";
    height: 0;
    overflow: hidden;
  }
  .footer-right {
    margin: 0 auto;
  }
  .footer a {
    color: white;
    padding: 5px;
    font-size: 10pt;
    margin: 0px 2px 0px 2px;
  }
  .textbox {
    width: 90vw;
  }

  @media only screen and (max-width: 900px) {
    .title {
      margin-bottom: 1rem;
    }
    p {
      border: 2px solid lightgray;
      border-radius: 0.5rem;
      padding: 1rem 1.5rem;
      margin: 0rem 0rem 1.5rem 0rem;
      background-color: white;
    }
    .progressbar-inner,
    .progressbar-outer,
    .typebox {
      width: 90vw;
    }
  }
</style>

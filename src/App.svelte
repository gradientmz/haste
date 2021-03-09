<script>
  var text = "This is some example text!";
  var typed = "";
  var correct = true;
  var progress = 0;
  var inputdisabled = false;
  var bgcolor = "";

  function type() {
    // Checks if typed charcters are correct
    bgcolor = "background-color: #fff";
    if (typed.slice(0, typed.length) == text.slice(0, typed.length)) {
      console.log("String is correct!");

      progress = (typed.length / text.length) * 100;

      // Check if the quote has been completed
      if (typed.length == text.length && typed == text) {
        console.log("String typed successfully!");
        inputdisabled = true;
        typed = "2.0s | 999 WPM";
        bgcolor = "background-color: #ccffe6";
      }
    } else {
      console.log("There's been a typing mistake...");
      bgcolor = "background-color: #ffcccc";
    }
  }

  function restart() {
    progress = 0;
    typed = "";
    inputdisabled = false;
    bgcolor = "#fff";
  }
</script>

<svelte:head>
  <script
    src="https://kit.fontawesome.com/347d7d5619.js"
    crossorigin="anonymous"></script>
</svelte:head>

<body style={bgcolor}>
  <div />
  <div>
    <h1 class="title">Haste</h1>
    <div class="textbox">
      <p>
        {text}
      </p>
    </div>
    <div class="progressbar-outer">
      <div class="progressbar-inner" style="width: {progress}%" />
    </div>
    <input
      class="typebox"
      disabled={inputdisabled}
      placeholder="Type here!"
      bind:value={typed}
      on:input={type}
    />
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
			<a href="https://twitter.com/gradientapps">Repo</a>
    </span>
  </div>
</body>

<style>
  @import url("https://fonts.googleapis.com/css2?family=Inter&display=swap");

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
  .textbox {
    width: 100%;
  }
  p {
    text-align: center;
    font-size: 1.25rem;
  }
  .typebox {
    font-size: 1.25rem;
    padding: 1rem 1rem;
    border: 1px solid gray;
    width: 60vw;
    border: 2px solid lightgray;
    border-radius: 0.5rem;
    background-color: whitesmoke;
  }
  .restartdiv {
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .restart {
    font-size: 1.5rem;
    margin-top: 1rem;
    border: 2px solid lightgray;
    border-radius: 0.5rem;
    padding: 0.5rem 1rem;
  }
  .progressbar-outer {
    height: 0.75rem;
    width: 60vw;
    margin-bottom: 0.75rem;
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
    font-color: white;
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
</style>

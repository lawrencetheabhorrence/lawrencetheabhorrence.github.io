<script lang="ts">
</script>

<main>
  <section class="socials-header">
    <h1>Cheska Huang</h1>
    <a href="https://www.linkedin.com/in/jfchuang/"
      ><img alt="LinkedIn" src="/pixel_linkedin.svg" /></a
    >
    <a href="https://github.com/lawrencetheabhorrence"
      ><img alt="GitHub" src="/pixelarticons_github.svg" /></a
    >
    <a href="mailto:julyannahuang@gmail.com"
      ><img alt="Email" src="/pixelarticons_mail.svg" /></a
    >
  </section>
  <nav>
    <img src="/cross.svg" />
    <ul class="links">
      <li>About</li>
      <li>Projects</li>
      <li>Experience</li>
    </ul>
  </nav>
  <section class="about-me">
    <p>
      Lorem ipsum dolor sit, amet consectetur adipisicing elit. Aperiam
      voluptates sapiente, excepturi dolores id accusamus. Nisi voluptatum
      deleniti soluta placeat adipisci. Nulla eius consequatur, laborum adipisci
      similique totam perferendis fuga.
    </p>
  </section>
  <section class="projects-header">
    <h2>Projects</h2>
  </section>
  <section class="projects">
    <article class="project item">
      <div></div>
      <article class="project-card">
        <h3>Project Name</h3>
        <p>A bit of sample text about the project</p>
      </article>
    </article>
  </section>
</main>

<style>
  main {
    background: top left / 8px repeat url("/bgtile.svg");
    box-shadow:
      0px 0px 138px 152px rgba(0, 0, 0, 0.05) inset,
      0px 0px 158px 27px rgba(0, 0, 0, 0.11) inset;
    width: 100vw;
    max-width: 100vw;
    min-height: 100vh;
    padding: 10vh 15vw 5vh 15vw;
    display: flex;
    flex-flow: column nowrap;
    align-items: stretch;
  }

  .socials-header {
    display: flex;
    align-items: baseline;
    gap: 4px;
    height: min-content;
  }

  .socials-header h1 {
    font-family: "Jersey 25", sans-serif;
    font-size: 3rem;
    margin: 0;
    margin-right: 0.5rem;
    text-shadow: 0 3px 0 rgba(76, 37, 37, 0.28);
    color: #5c4c43;
  }

  .socials-header img {
    width: 1.2rem;
  }

  nav {
    align-self: flex-start;
    display: flex;
    gap: 4px;
  }

  nav img[src="/cross.svg"] {
    width: 1rem;
  }

  nav ul {
    display: flex;
    list-style-type: none;
    flex-grow: 1;
  }

  nav ul > li {
    margin-right: 10px;
    background: #5c4c43;
    padding: 2px 8px;
    color: white;
    font-family: "Jersey 15", sans-serif;
    font-size: 1rem;
    text-transform: uppercase;
    box-shadow: 4px 4px 0 0 rgba(89, 74, 66, 0.28);
  }

  section.about-me {
    margin-left: 10%;
    background: #74675c;
    padding: 2%;
    box-shadow: 8px 8px 0 0 rgba(71, 52, 41, 0.43);
  }

  section.about-me > p {
    font-family: "Jersey 15", sans-serif;
    color: white;
    text-align: left;
  }

  article.project-card {
    width: 10vw;
    min-width: 108px;
    box-shadow: 4px 4px 0 0 rgba(92, 76, 67, 0.26);
  }

  article.project-card > * {
    width: 100%;
    font-family: "Jersey 15", sans-serif;
    font-size: 1rem;
    margin: 0;
  }

  article.project-card h3 {
    color: white;
    background: #5c4c43;
    text-transform: uppercase;
    text-align: center;
    padding: 2%;
  }

  article.project-card p {
    color: #463932;
    background: #fcfaf3;
    padding: 4%;
  }
</style>

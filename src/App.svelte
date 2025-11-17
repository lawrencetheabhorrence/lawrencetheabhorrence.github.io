<script lang="ts">
  import { sitedata } from "./sitedata";
  let navHeight: number | undefined = $state();
  let socialsHeight: number | undefined = $state();
  let aboutHeight: number | undefined = $state();
  let about: HTMLElement | undefined = $state();
  let aboutOffset = $derived(about?.offsetTop);

  let projectHeight: number | undefined = $state();
  let projectHeaderHeight: number | undefined = $state();
  let otherHeaderHeight: number | undefined = $state();
  let otherHeight: number | undefined = $state();
  let projectLineTop = $derived(
    (socialsHeight ?? 0) +
      (navHeight ?? 0) +
      (aboutHeight ?? 0) +
      (projectHeaderHeight ?? 0) +
      10,
  );

  let resumeHeaderHeight: number | undefined = $state();
  let otherLineTop = $derived(
    projectLineTop + (projectHeight ?? 0) + (otherHeaderHeight ?? 0) + 15,
  );
</script>

<main id="main">
  <div>
    <div class="node-line" style="top: {(aboutOffset ?? 0) - 15}px; left: 5px;">
      <div
        class="vert-line"
        style:height|important="{(aboutHeight ?? 0) +
          15 +
          Math.floor((projectHeaderHeight ?? 0) / 2)}px"
      ></div>
      <div
        class="vert-line"
        style="height: 22px; transform: rotate(-30deg);"
      ></div>
      <div class="line"></div>
      <div class="diamond"></div>
    </div>
    <div
      class="node-line"
      style="top: {projectLineTop}px; right: 5px; transform: scaleX(-1); transform-origin: bottom center;"
    >
      <div
        class="vert-line"
        style:height|important="{(projectHeight ?? 0) +
          10 +
          Math.floor((otherHeaderHeight ?? 0) / 2)}px"
      ></div>
      <div
        class="vert-line"
        style="height: 22px; transform: rotate(-30deg);"
      ></div>
      <div class="line"></div>
      <div class="diamond"></div>
    </div>
    <div class="node-line" style="top: {otherLineTop}px; left: 5px;">
      <div
        class="vert-line"
        style:height|important="{(otherHeight ?? 0) -
          8 +
          Math.floor((resumeHeaderHeight ?? 0) / 2)}px"
      ></div>
      <div
        class="vert-line"
        style="height: 22px; transform: rotate(-30deg);"
      ></div>
      <div class="line"></div>
      <div class="diamond"></div>
    </div>
    <section bind:offsetHeight={socialsHeight} id="socials-header">
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
    <nav bind:offsetHeight={navHeight}>
      <img src="/cross.svg" />
      <div class="line" />
      <ul class="links">
        <li><a href="#about-me">About</a></li>
        <li><a href="#projects">Projects</a></li>
        <li>Resume</li>
      </ul>
    </nav>
    <section bind:this={about} bind:offsetHeight={aboutHeight} id="about-me">
      <p>
        Lorem ipsum dolor sit, amet consectetur adipisicing elit. Aperiam
        voluptates sapiente, excepturi dolores id accusamus. Nisi voluptatum
        deleniti soluta placeat adipisci. Nulla eius consequatur, laborum
        adipisci similique totam perferendis fuga.
      </p>
    </section>
    <section
      bind:offsetHeight={projectHeaderHeight}
      id="projects-header"
      class="section-header"
    >
      <h2>Projects</h2>
      <div class="line"></div>
      <img src="/cross.svg" />
    </section>
    <section bind:offsetHeight={projectHeight} id="projects">
      {#each sitedata.projects as project}
        <article class="project-item">
          <img src={project.image ?? "/placeholder.svg"} />
          <article class="project-card">
            <h3>{project.name}</h3>
            <p>{project.description}</p>
          </article>
        </article>
      {/each}
    </section>
    <section
      bind:offsetHeight={otherHeaderHeight}
      id="other-projects-header"
      class="section-header"
    >
      <img src="/cross.svg" />
      <div class="line"></div>
      <h2>OTHER WORKS</h2>
    </section>
    <section bind:offsetHeight={otherHeight} id="other-projects">
      {#each sitedata.otherProjects as project}
        <article class="project-card">
          <h3>{project.name}</h3>
          <p>{project.description}</p>
        </article>
      {/each}
    </section>
    <section
      bind:offsetHeight={resumeHeaderHeight}
      id="resume-header"
      class="section-header"
    >
      <h2>Resume</h2>
      <img src="/memory_paperclip.svg" />
    </section>
    <section id="resume">
      {#each sitedata.resume as job}
        <article class="position-row">
          <p>{job.date}: {job.position}</p>
          <p>{job.organization}</p>
        </article>
      {/each}
    </section>
    <a href="#main">
      <section id="end">
        <p>Back to top</p>
        <img src="/ground.svg" />
      </section>
    </a>
  </div>
</main>

<style>
  main {
    width: 100%;
    margin-top: 5vh;
    max-width: 100%;
    min-height: 100vh;
    display: flex;
    flex-flow: column nowrap;
    align-items: center;
  }

  a {
    color: white;
  }

  main > div {
    width: 60%;
    min-width: 400px;
    position: relative;
  }

  #socials-header {
    display: flex;
    align-items: baseline;
    gap: 4px;
    height: min-content;
  }

  #socials-header h1 {
    font-family: "Jersey 25", sans-serif;
    font-size: 4rem;
    margin: 0;
    margin-right: 0.5rem;
    text-shadow: 0 3px 0 rgba(76, 37, 37, 0.28);
    color: #5c4c43;
  }

  #socials-header img {
    width: 1.2rem;
  }

  nav {
    align-self: flex-start;
    display: flex;
    gap: 4px;
    position: relative;
  }

  .line {
    box-shadow: none;
    background-color: #846a5b;
    height: 3px;
  }

  nav .line {
    background-color: #846a5b;
    z-index: 0;
    width: 99%;
    left: 12px;
    top: 46%;
    position: absolute;
  }

  nav > * {
    z-index: 5;
  }

  img[src="/cross.svg"] {
    width: 1rem;
  }

  nav ul {
    display: flex;
    list-style-type: none;
    flex-grow: 1;
  }

  p,
  h3 {
    font-family: "Jersey 15", sans-serif;
    font-size: 1.5rem;
  }

  h2 {
    font-family: "Jersey 20", sans-serif;
    color: #73665b;
    font-size: 2.5rem;
    text-shadow: -4px 5px 0 rgba(76, 37, 37, 0.2);
    text-transform: uppercase;
    margin: 0;
  }

  nav ul > li {
    margin-right: 10px;
    background: #5c4c43;
    padding: 2px 8px;
    color: white;
    font-family: "Jersey 15", sans-serif;
    font-size: 1.5rem;
    text-transform: uppercase;
    box-shadow: 4px 4px 0 0 rgba(89, 74, 66, 0.28);
  }

  section#about-me {
    margin-left: 3%;
    background: #74675c;
    padding: 2%;
    box-shadow: 8px 8px 0 0 rgba(71, 52, 41, 0.43);
    margin-bottom: 20px;
  }

  section#about-me > p {
    font-family: "Jersey 15", sans-serif;
    color: white;
    text-align: left;
  }

  section#projects {
    padding-right: 0%;
  }

  article.project-card {
    width: 30%;
    min-width: 150px;
    box-shadow: 4px 4px 0 0 rgba(92, 76, 67, 0.26);
  }

  article.project-card > * {
    width: 100%;
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

  #about-me {
    border-left: 3px solid #846a5b;
  }

  .project-item {
    display: flex;
    padding-right: 5%;
    width: 100%;
    align-items: flex-start;
    margin-bottom: 2vh;
  }

  .project-item > img {
    flex-grow: 1;
    margin-right: 3%;
    border-radius: 12px;
    max-width: 70%;
    box-shadow: 4px 4px 0.3px 0 rgba(190, 176, 164, 0.92);
  }

  .position-row {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 4px 16px;
    box-shadow: 4px 4px 0 0 rgba(92, 76, 67, 0.26);
    margin-bottom: 8px;
  }

  .position-row:nth-child(odd) {
    background: #5c4c43;
    color: white;
  }

  .position-row:nth-child(even) {
    background: white;
    color: #5c4c43;
  }

  .position-row p {
    text-transform: uppercase;
    margin: 0;
  }

  #end p {
    color: rgba(115, 102, 91, 0.76);
    text-transform: uppercase;
    margin: 20vh 0 0 0;
  }

  #end img {
    width: 20px;
  }

  .section-header {
    display: flex;
    align-items: center;
  }

  div.line {
    flex-grow: 1;
    background-color: #846a5b;
    height: 3px;
    box-shadow: 0 2px 0 rgba(44, 24, 24, 0.25);
    margin: 0 4px;
    border-radius: 9999px;
  }

  #projects-header,
  #resume-header {
    padding-left: 10%;
  }

  #other-projects-header {
    padding-right: 10%;
  }

  #other-projects {
    padding: 8px 2%;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    margin-left: 5%;
    gap: 2%;
    place-items: center;
  }

  #other-projects .project-card {
    width: 100%;
    height: 100%;
    display: flex;
    flex-flow: column nowrap;
  }

  #other-projects .project-card p {
    flex-grow: 1;
  }

  .node-line {
    position: absolute;
    width: 5%;
    min-width: 32px;
  }
  div.vert-line {
    width: 3px;
    background-color: #846a5b;
    transform-origin: top left;
  }

  .node-line .line {
    box-shadow: none;
    background-color: #846a5b;
    width: 90%;
    border-radius: 0;
    height: 3px;
    position: relative;
    bottom: 6px;
    left: 7px;
  }

  .node-line .diamond {
    width: 12px;
    aspect-ratio: 1 / 1;
    background-color: #846a5b;
    transform: rotate(45deg);
    position: absolute;
    bottom: 2px;
    left: 90%;
  }
</style>

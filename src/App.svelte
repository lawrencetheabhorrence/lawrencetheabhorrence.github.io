<script lang="ts">
  import { onMount } from "svelte";
  import { sitedata } from "./sitedata";
  import TypeIt from "typeit";
  import { animate, stagger } from "animejs";

  const options = {
    strings: [
      "Hi! I'm Cheska, a third-year Computer Science student who builds stuff.",
    ],
    speed: 40,
    waitUntilVisible: true,
  };

  onMount(() => {
    new TypeIt("#about-p", options).go();
  });

  let mainWidth: number | undefined = $state();
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

<main bind:offsetWidth={mainWidth} id="main">
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
        <li><a href="#projects-header">Projects</a></li>
        <li><a href="#resume-header">Resume</a></li>
      </ul>
    </nav>
    <section bind:this={about} bind:offsetHeight={aboutHeight} id="about-me">
      <div class="about-cont">
        <p id="about-p" style="text-align: center;"></p>
      </div>
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
          <video autoplay loop src={project.video ?? "/placeholder-ps.webm"}>
          </video>
          <article class="project-card">
            <div class="project-cardheader">
              <h3>{project.name}</h3>
              {#if project.link}
                <a href={project.link}>
                  <svg
                    fill="white"
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 24 24"
                  >
                    <path
                      d="M4 6h7v2H4v8h7v2H2V6h2zm16 0h-7v2h7v8h-7v2h9V6h-2zm-3 5H7v2h10v-2z"
                      fill="currentColor"
                    />
                  </svg>
                </a>
              {/if}
            </div>
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
      {#each sitedata.otherProjects as project, ix}
        <article class="project-card">
          <div class="project-cardheader">
            <h3>{project.name}</h3>
            {#if project.link}
              <a href={project.link}>
                <svg
                  fill="white"
                  xmlns="http://www.w3.org/2000/svg"
                  viewBox="0 0 24 24"
                >
                  <path
                    d="M4 6h7v2H4v8h7v2H2V6h2zm16 0h-7v2h7v8h-7v2h9V6h-2zm-3 5H7v2h10v-2z"
                    fill="currentColor"
                  />
                </svg>
              </a>
            {/if}
          </div>
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
      <a href={sitedata.resumeLink}><img src="/memory_paperclip.svg" /></a>
    </section>
    <section id="resume">
      {#each sitedata.resume as job, i}
        <article class="position-row" style:width|important={mainWidth}>
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
    transition: 450ms cubic-bezier(0.44, 0, 0.56, 1) text-shadow;
    color: #5c4c43;
  }

  #socials-header:hover h1 {
    text-shadow: 2px 5px 0 rgba(76, 37, 37, 0.28);
  }

  #socials-header img {
    width: 22px;
    transition: 350ms cubic-bezier(1, 0, 0, 1) all;
  }

  #socials-header img:hover {
    transform: scale(1.3) translateY(-2px);
    margin-right: 4px;
    margin-left: 4px;
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
    text-shadow: -3px 3px 0 rgba(76, 37, 37, 0.2);
    text-transform: uppercase;
    transition: 250ms ease-in-out text-shadow;
    margin: 0;
  }

  h2:hover {
    text-shadow: -5px 5px 0 rgba(76, 37, 37, 0.2);
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
    transition: 350ms cubic-bezier(1, 0, 0, 1) all;
  }

  nav ul > li:hover {
    padding: 2px 16px;
    margin-right: 12px;
  }

  section#about-me {
    margin-left: 3%;
    background: #74675c;
    padding: 2%;
    box-shadow: 8px 8px 0 0 rgba(71, 52, 41, 0.43);
    margin-bottom: 20px;
    transform-origin: top left;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  section#about-me p {
    font-family: "Jersey 15", sans-serif;
    width: 100%;
    font-size: 1.5rem;
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
    transition: 350ms ease-in-out all;
    animation:
      1000ms cubic-bezier(0.86, 0, 0.14, 1) 0s listItemEnter,
      1000ms cubic-bezier(1, 0, 0, 1) 0ms shadowEnter;
  }

  .project-item:hover > article.project-card,
  article.project-card:hover {
    box-shadow: 8px 8px 0 0 rgba(92, 76, 67, 0.26);
  }

  article.project-card > * {
    width: 100%;
    margin: 0;
  }

  article.project-card .project-cardheader {
    color: white;
    background: #5c4c43;
    text-transform: uppercase;
    text-align: center;
    padding: 2px 8px;
    display: flex;
    align-items: center;
    justify-content: space-evenly;
  }

  .project-cardheader h3 {
    padding: 0;
  }
  .project-cardheader svg {
    width: 20px;
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

  .project-item > video {
    flex-grow: 1;
    margin-right: 3%;
    border-radius: 12px;
    max-width: 70%;
    box-shadow: 4px 4px 0.3px 0 rgba(190, 176, 164, 0.92);
    transition: 350ms ease-in-out all;
  }

  .project-item:hover > video {
    box-shadow: 8px 8px 0.3px 0 rgba(190, 176, 164, 0.92);
  }

  .position-row {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 4px 16px;
    width: 60vw;
    box-shadow: 4px 4px 0 0 rgba(92, 76, 67, 0.26);
    margin-bottom: 12px;
    transform-origin: top center;
    transition: 250ms ease-in-out all;
  }

  .position-row:hover {
    padding: 16px 16px;
    box-shadow: 4px 6px 0 0 rgba(92, 76, 67, 0.26);
    margin-bottom: 14px;
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
    font-size: clamp(12px, 2vw, 20px);
    margin: 0;
  }

  #resume {
    margin-bottom: 30vh;
  }
  #end {
    display: flex;
    flex-flow: column nowrap;
    align-items: center;
    width: 100%;
    position: absolute;
    bottom: 12px;
  }

  #end p {
    color: rgba(115, 102, 91, 0.76);
    text-transform: uppercase;
    margin: 20vh 0 0 0;
    transition: 250ms ease-in-out color;
  }

  #end img {
    width: 28px;
    transition: 250ms ease-in-out filter;
  }

  #end:hover p {
    color: #7c6e64;
  }

  #end:hover img {
    filter: brightness(0) saturate(100%);
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

  #resume-header img {
    transform: rotate(-6deg);
    transition: 300ms cubic-bezier(0.44, 0, 0.56, 1) all;
    transform-origin: bottom center;
  }

  #resume-header a:hover img {
    transform: rotate(-12deg) translateY(-2px);
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

  @keyframes shadowEnter {
    from {
      box-shadow: 0px 0px 0 0 rgba(92, 76, 67, 0.26);
    }
    to {
      box-shadow: 4px 4px 0 0 rgba(92, 76, 67, 0.26);
    }
  }
  @keyframes listItemEnter {
    from {
      clip-path: polygon(0% 0%, 0% 0%, 0% 0%, 0% 0%);
    }

    to {
      clip-path: polygon(0% 0%, 115% 0%, 115% 115%, 0% 115%);
    }
  }
</style>

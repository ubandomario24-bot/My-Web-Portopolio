<template>
<nav class="navbar navbar-dark bg-dark">
  <div class="container-fluid">
    <a class="navbar-brand" href="#"><img src="https://static.vecteezy.com/system/resources/thumbnails/027/969/749/small/cute-illustration-designs-for-the-characters-in-the-super-mario-bros-game-free-vector.jpg" width="50" height="50"></a>

    <div class="d-flex align-items-center">
      
      <ul class="navbar-nav flex-row d-none d-lg-flex me-3">
        <li class="nav-item px-2"><a class="nav-link" href="#landing">Home</a></li>
        <li class="nav-item px-2"><a class="nav-link" href="#projects">My Projects</a></li>
        <li class="nav-item px-2"><a class="nav-link" href="#tools">Tools</a></li>
        <li class="nav-item px-2"><a class="nav-link" href="#contact">Contacts</a></li>
        <li class="nav-item px-2"><a class="nav-link" href="/Resume.pdf" target="_blank">Resume</a></li>
      </ul>

      <button class="sidebar-toggler bg-dark" type="button" data-bs-toggle="offcanvas" data-bs-target="#sidebarMenu">
        <span class="navbar-toggler-icon"></span>
      </button>
      
    </div>
  </div>
</nav>
<div class="offcanvas offcanvas-end text-bg-dark" tabindex="-1" id="sidebarMenu">
  <div class="offcanvas-header border-bottom border-secondary bg-dark">
    <h5 class="offcanvas-title text-white">Side Menu</h5>
    <button type="button" class="btn-close btn-close-white" data-bs-dismiss="offcanvas"></button>
  </div>
  <div class="offcanvas-body bg-dark">
    <ul class="nav flex-column gap-2">
      <li class="nav-item d-lg-none"> <a class="nav-link text-white" href="#landing">Home</a>
        <a class="nav-link text-white" href="#projects">My Projects</a>
        <a class="nav-link text-white" href="#toolz">Tools</a>
        <a class="nav-link text-white" href="#contact">Contacts</a>
        <a class="nav-link text-white" href="Resume.pdf">Resume</a>
        <hr>
      </li>
    </ul>
  </div>
</div>
</template>

---
layout: default
title: "Antoine Camerlo - Systems Engineer"
description: "Personal portfolio of Antoine Camerlo, Systems Engineer specializing in DevOps and infrastructure solutions."
---

<div id="main-content">
  <main role="main" aria-label="Main content">
    <section class="hero container text-center" aria-labelledby="hero-heading">
      <h1 id="hero-heading">Antoine Camerlo</h1>
      <p class="subtitle" role="doc-subtitle">Systems Engineer</p>
      
      <div class="social-links" role="navigation" aria-label="Social media links">
        {% if site.github-user %}
          <a href="https://github.com/{{ site.github-user }}" aria-label="GitHub profile" class="social-link">
            <span class="fab fa-github fa-2x"></span>
          </a>
        {% endif %}
        
        {% if site.twitter %}
          <a href="https://twitter.com/{{ site.twitter }}" aria-label="Twitter profile" class="social-link">
            <span class="fab fa-twitter fa-2x"></span>
          </a>
        {% endif %}
        
        {% if site.linkedin %}
          <a href="https://linkedin.com/in/{{ site.linkedin }}" aria-label="LinkedIn profile" class="social-link">
            <span class="fab fa-linkedin fa-2x"></span>
          </a>
        {% endif %}
        
        {% if site.email %}
          <a href="mailto:{{ site.email }}" aria-label="Email" class="social-link">
            <span class="fas fa-envelope fa-2x"></span>
          </a>
        {% endif %}
      </div>
    </section>
    
    <section class="about container mt-5" aria-labelledby="about-heading">
      <h2 id="about-heading">About Me</h2>
      <div class="about-content">
        <p>I'm a passionate Systems Engineer with expertise in DevOps, infrastructure automation, and cloud computing.</p>
        <p>This portfolio showcases my projects, skills, and professional journey.</p>
      </div>
    </section>
  </main>
</div>

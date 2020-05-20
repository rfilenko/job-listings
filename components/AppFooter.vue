<template>
  <footer>
    <div class="attribution">
      <p>
        Challenge by
        <a
          href="https://www.frontendmentor.io?ref=challenge"
          target="_blank"
        >Frontend Mentor</a>.
      </p>
      <p>
        Coded by
        <a href="https://rfilenko-cv.netlify.app/">@Roman Filenko</a>.
      </p>
    </div>
  </footer>
</template>
<style>
footer {
  margin-top: auto;
  background: var(--primary-clr);
  color: var(--accent-clr);
  padding: 1rem;
  font-size: 0.75rem;
  display: flex;
  justify-content: center;
}
footer a:hover {
  text-decoration-style: double;
}
.attribution {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.attribution p + p {
  margin-bottom: 0.5rem;
}
</style>

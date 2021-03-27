<template>
  <footer class="footer mt-5">
    <hr />
    <div class="container mt-4">
      <div class="row">
        <div class="col-sm">
          <p class="align-middle text-left text-muted">
            <strong
              >Hoop-Boop is an app where loved ones can see and mark the
              memories they share. Created by
              <a
                target="_blank"
                rel="noopener noreferrer"
                href="https://www.instagram.com/ritwikdiv/"
                >Ritwik Divakaruni</a
              >
              with
              <svg
                xmlns="http://www.w3.org/2000/svg"
                width="15"
                height="15"
                fill="#C0B9DD"
                class="bi bi-heart-fill"
                viewBox="0 0 16 16"
              >
                <path
                  fill-rule="evenodd"
                  d="M8 1.314C12.438-3.248 23.534 4.735 8 15-7.534 4.736 3.562-3.248 8 1.314z"
                />
              </svg>
            </strong>
          </p>
        </div>
        <div class="col-sm align-middle text-right">
          <a
            target="_blank"
            rel="noopener noreferrer"
            class="btn btn-outline-secondary btn-sm ml-3 mr-3"
            href="mailto:ritwik.social@gmail.com"
            role="button"
            ><strong>Talk to me!</strong></a
          >
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: "Footer",
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.footer {
  bottom: 20px;
}
</style>

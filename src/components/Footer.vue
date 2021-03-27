<template>
  <footer class="blog-footer">
    <hr />
    <div class="container align-top">
      <div class="row">
        <div class="col-sm">
          <p class="align-middle text-center text-muted">
            <strong
              >Created by
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
.blog-footer {
  bottom: 0px;
  background-color: white;
}

.btn-outline-regular {
  color: #355070;
  background-color: transparent;
  background-image: none;
  border-color: #355070;
}
.btn-outline-regular:hover {
  color: #fff;
  background-color: #355070;
  border-color: #355070;
}
.btn-outline-regular.focus,
.btn-outline-regular:focus {
  box-shadow: 0 0 0 0.2rem rgba(0, 123, 255, 0.5);
}
.btn-outline-regular.disabled,
.btn-outline-regular:disabled {
  color: #355070;
  background-color: transparent;
}
.btn-outline-regular:not(:disabled):not(.disabled).active,
.btn-outline-regular:not(:disabled):not(.disabled):active,
.show > .btn-outline-regular.dropdown-toggle {
  color: #fff;
  background-color: #355070;
  border-color: #355070;
}
.btn-outline-regular:not(:disabled):not(.disabled).active:focus,
.btn-outline-regular:not(:disabled):not(.disabled):active:focus,
.show > .btn-outline-regular.dropdown-toggle:focus {
  box-shadow: 0 0 0 0.2rem rgba(0, 123, 255, 0.5);
}
</style>

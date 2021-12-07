<template>
  <div class="hello">
    <div class="main-image">
      <img :src="require(`@/assets/carousel-background-image.svg`)"
           class="d-block w-100 img-fluid main-image-size"
           alt="..."
      >
    </div>
    <div id="carouselUsers" class="carousel slide" data-bs-ride="carousel" data-bs-interval="false">

      <div class="carousel-inner p-3">
        <div class="row">

            <div v-if="slides.length === 0">
              <img :src="require(`@/assets/no-image-found.png`)"
                   class="d-block w-100 img-fluid thumbnails-height"
                   alt="..."
              >
            </div>
            <div v-for="(doc, index) in slides"
                 :key="index"
                 :class="index === 0 ? 'active carousel-item' : 'carousel-item'"
                 :id="'carousel-inner-'+index"
            >
              <div class="col-3">
                <img v-if="getImage(doc.profile)" :src="require(`@/assets/${doc.profile}`)"
                     class="d-block w-100 img-fluid thumbnails-height"
                     alt="..."
                >
                <img v-else :src="require(`@/assets/no-image-found.png`)" class="d-block w-100 img-fluid thumbnails-img" alt="...">
              </div>
              <div class="col-9">
                <div class="carousel-caption d-md-block">
                  <p class="name-paragraph">{{ doc.name }} {{ doc.surname }}</p>
                  <p class="address-paragraph">{{ doc.address }}</p>
                </div>
              </div>
              <div class="row wrapper">
                <!-- Ideally we would pass a userId here, and then retrieve correct data in the Info component rather than
                 passing whole object in the url parameter (;.;) please dont blame me, time efficiency -->
                <router-link :to="{ name: 'Info', params: { user: doc }}"><button class="btn btn-outline-dark d-inline w-25 m-2 btn-rounded">Info</button></router-link>
                <button class="btn btn-primary d-inline w-25 m-2 btn-rounded">Contact</button>
              </div>
            </div>

        </div>
      </div>

      <button class="carousel-control-prev" type="button" :data-bs-target="'#carouselUsers'" data-bs-slide="prev">
        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
        <span class="visually-hidden">Previous</span>
      </button>
      <button class="carousel-control-next" type="button" :data-bs-target="'#carouselUsers'" data-bs-slide="next">
        <span class="carousel-control-next-icon" aria-hidden="true"></span>
        <span class="visually-hidden">Next</span>
      </button>

    </div>

  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      slides: [
        {
          name: 'Raf',
          surname: 'Test',
          address: 'London Office, UK',
          profile: 'Bitmap.png'
        },
        {
          name: 'Raf2',
          surname: 'Test2',
          address: 'Sheffield Office, UK',
          profile: 'logo.png'
        },
        {
          name: 'Raf3',
          surname: 'Test3',
          address: 'Scarborough Office, UK',
          profile: 'Bitmap.png'
        }
      ]
    }
  },
  methods: {
    getImage (fileName) {
      try {
        return require(`@/assets/${fileName}`)
      } catch (e) {
        return false
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.hello {
  width: 50%;
  height: auto;
  margin: auto;
  .main-image {
    width: 100%;
    height: auto;
    margin: 20px;
    .main-image-size {
      max-width: 50%;
      margin: auto;
    }
  }
  .name-paragraph {
    color: black;
    font-weight: bold;
    font-size: 16px;
  }
  .address-paragraph {
    color: black;
    font-size: 16px;
  }
  #carouselUsers {
    .carousel-control-prev-icon {
      background-image: url("data:image/svg+xml;charset=utf8,%3Csvg xmlns='http://www.w3.org/2000/svg' fill='%23000' viewBox='0 0 10 8'%3E%3Cpath d='M5.25 0l-4 4 4 4 1.5-1.5-2.5-2.5 2.5-2.5-1.5-1.5z'/%3E%3C/svg%3E");
    }

    .carousel-control-next-icon {
      background-image: url("data:image/svg+xml;charset=utf8,%3Csvg xmlns='http://www.w3.org/2000/svg' fill='%23000' viewBox='0 0 10 8'%3E%3Cpath d='M2.75 0l-1.5 1.5 2.5 2.5-2.5 2.5 1.5 1.5 4-4-4-4z'/%3E%3C/svg%3E");
    }

    .thumbnails-height {
      width: 100%;
      height: auto;
      border-radius: 50%;
    }

    .carousel-inner {
      width: 80%;
      margin: auto;
      border-radius: 5px;
      height: auto;
      background-clip: border-box;
      border: 1px solid rgba(0, 0, 0, .125);
      box-shadow: 0rem 1rem 1rem rgba(0, 0, 0, .25);
    }

    .carousel-caption {
      right: 15%;
      bottom: 3rem;
      left: 25%;
    }
  }

  /* change transition duration to control the speed of fade effect */
  .carousel-item {
    transition: transform 1s ease-in-out;
  }

  .carousel-fade .active.carousel-item-start,
  .carousel-fade .active.carousel-item-end {
    transition: opacity 1s 1s;
  }

  .wrapper {
    display: block;
    width: 100%;
    margin: auto;
    .btn-rounded {
      border-radius: 30px;
    }
  }
}

@media screen and (max-width: 640px) {
  .carousel-caption {
    right: 15%;
    bottom: 0 !important;
    left: 25%;
  }
  .btn-rounded {
    font-size: 9px;
  }
}

@media screen and (min-width: 641px) {
  .carousel-caption {
    right: 15%;
    bottom: 0 !important;
    left: 25%;
  }
  .btn-rounded {
    font-size: 11px;
  }
}

@media screen and (min-width: 1080px) {
  .carousel-caption {
    right: 15%;
    bottom: 3rem !important;
    left: 25%;
  }

  .btn-rounded {
    font-size: 16px;
  }
}
</style>

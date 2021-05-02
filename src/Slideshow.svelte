<script>
  // import Swiper core and required modules
  import SwiperCore, {
    A11y,
    Autoplay,
    Navigation,
    Pagination,
    Scrollbar,
  } from "swiper";
  import { Swiper, SwiperSlide } from "swiper/svelte";
  import NavCategories from "./components/navbar/NavCategories.svelte";

  // install Swiper modules
  SwiperCore.use([Navigation, Pagination, Scrollbar, A11y, Autoplay]);

  let imagePaths = [
    {
      path:
        "https://www.airholic.it/wp-content/uploads/DSC6016_copia.jpg",
      position: "center",
    },
    {
      path:
        "https://images.unsplash.com/photo-1483304528321-0674f0040030?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=3150&q=80",
      position: "center",
    },
    {
      path:
        "https://images.unsplash.com/photo-1484320775925-2609d111d8b3?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1949&q=80",
      position: "top",
    },
    {
      path:
        "https://images.unsplash.com/photo-1487692703274-4965f352a3ef?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1953&q=80",
      position: "center",
    },
  ];
</script>

<div class="relative">
  <Swiper
    spaceBetween={5}
    slidesPerView={1}
    navigation
    pagination
    loop
    autoplay={{ delay: 2500, disableOnInteraction: false }}
    watchSlidesVisibility
    watchSlidesProgress
    on:slideChange={() => console.log("slide change")}
  >
    {#each imagePaths as image}
      <SwiperSlide>
        <div
          style="background: linear-gradient(rgba(0, 0, 0, 0.6), rgba(0, 0, 0, 0.6)),
        url({image.path}); background-position: {image.position}"
          class="module mid w-full bg-center"
        >
          <h2 class="bg-gradient-to-r from-green-500 to-blue-500  ">
            Aviokimpex
          </h2>
        </div>
      </SwiperSlide>
    {/each}
  </Swiper>
  <NavCategories />
</div>

<style>
  .mid h2 {
    font-family: "Roboto", sans-serif;
    font-weight: 900;
    color: white;
    text-transform: uppercase;
    margin: 0;
    position: absolute;
    top: 50%;
    left: 50%;
    font-size: 2rem;
    transform: translate(-50%, -50%);
  }
  .module {
    background-size: cover;
    background-position: center;
    height: 66vh;

    position: relative;
    float: left;
  }
</style>

<script>
  import Modal from "./modal/Modal.svelte";
  import Content from "../Content.svelte";
  import { modal } from '../store/stores.js';
  import ListCategories from '../ListCategories.svelte';
  import FormEmail from './FormEmail.svelte';
</script>
<div class="flex flex-wrap space-y-4 md:space-y-0 flex-col md:flex-row items-center -mx-2 p-10">
    <div class="px-2 md:w-1/2 w-full">
    <div class="flex flex-wrap w-full bg-gray-100 sm:py-24 py-16 sm:px-10 px-6 relative">
        <img alt="gallery" class="w-full object-cover h-full object-center block opacity-40c absolute inset-0 filter md:blur-sm" src="images/engine-part.jpg">
        <div class="text-center relative z-10 w-full">
        <h2 class="text-xl text-gray-900 font-medium title-font mb-2">
            <span class="bg-gradient-to-r from-green-500 to-blue-500 card-title text-base md:text-xl lg:text-3xl">vasto assortimento</span>
        </h2>
        <Modal show={$modal}>
            <Content componentToRender={ListCategories}>
                <button class="mt-3 rounded inline-flex items-center text-white bg-green-400 border-0 py-2 px-4 focus:outline-none hover:bg-green-600">Consulta catalogo
                    <svg fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" class="w-4 h-4 ml-2" viewBox="0 0 24 24">
                    <path d="M5 12h14M12 5l7 7-7 7"></path>
                    </svg>
                </button>
            </Content>
        </Modal>
        </div>
    </div>
    </div>
    <div class="px-2 md:w-1/2 w-full">
    <div class="flex flex-wrap w-full bg-gray-100 sm:py-24 py-16 sm:px-10 px-6 relative">
        <img alt="gallery" class="w-full object-cover h-full object-center block opacity-40 absolute inset-0 filter md:blur-sm" src="images/front-view-plane.jpg">
        <div class="text-center relative w-full">
        <h2 class="text-xl text-gray-900 font-medium title-font mb-2">
            <span class="bg-gradient-to-r from-green-500 to-blue-500 card-title text-base md:text-xl lg:text-3xl">prezzi convenienti</span>
        </h2>
        <Modal show={$modal}>
            <Content componentToRender={FormEmail}>
                <button class="mt-3 rounded inline-flex items-center text-white bg-green-400 border-0 py-2 px-4 focus:outline-none hover:bg-green-600">Richiedi quotazione
                    <svg fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" class="w-4 h-4 ml-2" viewBox="0 0 24 24">
                    <path d="M5 12h14M12 5l7 7-7 7"></path>
                    </svg>
                </button>
            </Content>
        </Modal>
        </div>
    </div>
    </div>
</div>
<style>
    .card-title {
        font-family: "Roboto", sans-serif;
        font-weight: 900;
        color: white;
        text-transform: uppercase;
    }
</style>
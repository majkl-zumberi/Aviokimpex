<script>
  import { _ } from "svelte-i18n";
  import { Doc } from "sveltefire";
  import ArticleListContainer from "./ArticleListContainer.svelte";
  import ListCategories from "../../ListCategories.svelte";
  import * as emailjs from 'emailjs-com';
  import { toast } from '@zerodevx/svelte-toast'

  let articleMessage='';
  export let params = {};
  function mapArticleToMessageEmail(article){
    articleMessage=Object.keys(article)
    .map(articleDetail=>`${articleDetail}: ${article[articleDetail]}`)
    .join(", ");
  }
  function sendForm(event){
    const loadingToast=toast.push('Invio in corso...')
    emailjs.sendForm(_vars.env.emailjsServiceId, _vars.env.emailjsTemplateArticleId, event.target, _vars.env.emailjsUserId)
      .then((result) => {
        toast.pop(loadingToast);
        toast.push('Richiesta quotazione inviata con successo!', {
          theme: {
            '--toastBackground': '#48BB78',
            '--toastColor': '#FFFFFF',
            '--toastProgressBackground': '#2F855A'
          }
        });
        event.target.reset();
      }, (error) => {
        toast.push('Ops.. si è verificato un errore!', {
                theme: {
          '--toastBackground': '#F56565',
          '--toastColor': '#FFFFFF',
          '--toastProgressBackground': '#C53030'
        }
        })
      });
  }
</script>

<section class="text-gray-600 body-font">
  <div class="container px-5 py-24 mx-auto">
    <div class="flex flex-wrap -m-4">
      <div class="p-4 lg:w-1/3 w-full">
        <div
          class="h-full  bg-opacity-75 px-8      pb-24 rounded-lg overflow-hidden text-center relative"
        >
          <ListCategories />
        </div>
      </div>
      <Doc path={`articoli/${params.id}`} let:data={articleItem}>
        <!-- Default Slot -->
        <ArticleListContainer
          article={articleItem}
          isInList={false}
          viewLink={false}
          on:articleDetail={(article)=>mapArticleToMessageEmail(article.detail.article)}
        />

        <!-- Only shown when loading -->
        <div slot="loading" />

        <!-- Shown on error or if nothing loads after maxWait time-->
        <div slot="fallback" />
      </Doc>

      <div class="p-4 lg:w-1/3 sm:w-full">
        <div
          class=" bg-gray-100 rounded-lg p-8 flex flex-col md:ml-auto w-full mt-10 md:mt-0"
        >
          <h2 class="text-gray-900 text-lg font-medium title-font mb-5">
            {$_("order.request", {
              default: "Richiedi quotazione",
            })}
          </h2>
          <h3 class="text-gray-500 text-base  title-font mb-5">
            {$_("order.info", {
              default:
                "Vuoi ricevere maggiori informazioni o una quotazione personalizzata su questo articolo? Chiamaci al numero",
            })} <span class="font-medium">+390302421830</span>
            {$_("order.fillForm", {
              default: "oppure compila il form",
            })}
          </h3>
          <form on:submit|preventDefault={sendForm}>
            <div class="relative mb-4">
              <label for="from_name" class="leading-7 text-sm text-gray-600">
                {$_("order.fullName", {
                  default: "Nome e cognome",
                })}
              </label>
              <input
                type="text"
                id="from_name"
                name="from_name"
                class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
              />
            </div>
            <div class="relative mb-4">
              <label for="from_email" class="leading-7 text-sm text-gray-600"
                >Email</label
              >
              <input
                type="email"
                id="from_email"
                name="from_email"
                class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
              />
            </div>
            <div class="relative mb-4">
              <label for="phone_number" class="leading-7 text-sm text-gray-600">
                {$_("order.phone", {
                  default: "Telefono",
                })}
              </label>
              <input
                type="text"
                id="phone_number"
                name="phone_number"
                class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
              />
              <input type="hidden" name="message" bind:value={articleMessage}>
            </div>
            <button
              type="submit"
              class="text-white uppercase bg-green-400 border-0 py-2 px-8 focus:outline-none hover:bg-green-600 rounded text-lg"
            >
              {$_("order.submit", {
                default: "Invia",
              })}
            </button>
        </form>
        </div>
      </div>
    </div>
  </div>
</section>

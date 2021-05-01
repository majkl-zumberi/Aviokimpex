<script>
  import { _ } from "svelte-i18n";
  import * as emailjs from 'emailjs-com';
  import { toast } from '@zerodevx/svelte-toast'
  function sendForm(event){
    console.log({event})
    const loadingToast=toast.push('Invio in corso...')
    emailjs.sendForm(_vars.env.emailjsServiceId, _vars.env.emailjsTemplateId, event.target, _vars.env.emailjsUserId)
      .then((result) => {
        toast.pop(loadingToast);
        toast.push('Email inviata con successo!', {
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


<!-- GOOGLE MAPS API WITH FEEDBACK FORM -->

  <section class="text-gray-600 body-font relative">

    <div class="container px-5 py-24 mx-auto flex flex-col md:flex-nowrap md:flex-row flex-wrap">
      <div class="lg:w-2/3 md:w-1/2 min-h-screen md:min-h-full bg-gray-300 rounded-lg overflow-hidden sm:mr-10 p-10 flex items-end justify-start relative">
        <iframe width="100%" height="100%" class="absolute inset-0" frameborder="0" title="map" marginheight="0" marginwidth="0" scrolling="no" src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d320.39210876336256!2d10.224536431952265!3d45.527783728327634!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x4781760e995540f7%3A0x71296509d6f55da0!2sVia%20Raffaele%20da%20Brescia%2C%2025%2C%2025124%20Brescia%20BS!5e0!3m2!1sit!2sit!4v1614285489545!5m2!1sit!2sit" style="filter: grayscale(1) contrast(1) opacity(0.7);"></iframe>
      </div>
      <div class="lg:w-1/3 md:w-1/2 bg-white flex flex-col md:ml-auto w-full md:py-8 mt-8 md:mt-0">
        <h2 class="text-gray-900 text-lg mb-1 font-medium title-font">Feedback</h2>
        <p class="leading-relaxed mb-5 text-gray-600">{$_("contacts.thanks", {
          default:
            "Grazie per averci contattato",
        })}</p>
        <form on:submit|preventDefault={sendForm}>
          <div class="relative mb-4">
            <label for="from_name" class="leading-7 text-sm text-gray-600">{$_("contacts.name", {
              default:
                "Nome",
              })}</label>
            <input type="text" id="from_name" name="from_name" class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out">
          </div>
          <div class="relative mb-4">
            <label for="from_email" class="leading-7 text-sm text-gray-600">{$_("contacts.email", {
              default:
                "Email",
              })}</label>
            <input type="email" id="from_email" name="from_email" class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out">
          </div>
          <div class="relative mb-4">
            <label for="name" class="leading-7 text-sm text-gray-600">{$_("contacts.message", {
              default:
                "Messaggio",
              })}</label>
            <textarea id="message" name="message" class="w-full bg-white rounded border border-gray-300 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 h-32 text-base outline-none text-gray-700 py-1 px-3 resize-none leading-6 transition-colors duration-200 ease-in-out"></textarea>
          </div>
          <button type="submit" class="text-white bg-indigo-500 border-0 py-2 px-6 focus:outline-none hover:bg-indigo-600 rounded text-lg">{$_("contacts.send", {
            default:
              "Invia",
            })}</button>
          </form>
          <p class="text-xs text-gray-500 mt-3">{$_("contacts.soon", {
            default:
              "Ti contatteremo nel minor tempo possibile.",
            })}</p>
      </div>
    </div>
  </section>
  <style>
    :root {
    --toastBackground: rgba(255,255,255,0.95);
    --toastColor: #424242;
    --toastProgressBackground: aquamarine;
  }
  </style>
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
<div class=" bg-gray-100 rounded-lg p-8 flex flex-col md:ml-auto w-full mt-10 md:mt-0">
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
       <div class="relative text-left mb-4">
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
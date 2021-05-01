<script>
    import { getContext } from 'svelte';
    import { fly } from 'svelte/transition';
      
    import Popup from './components/modal/Popup.svelte';
    
    import CloseButton from './components/modal/CloseButton.svelte';
  
    const { open } = getContext('simple-modal');
      export let componentToRender = Popup
      let opening = false;
      let opened = false;
      let closing = false;
      let closed = false;
  
    const showPopup = () => {
          open(componentToRender, { message: "It's a popup!" });
      };
      
      let name;
      let status = 0;
      
      const onCancel = (text) => {
          name = '';
          status = -1;
      }
      
      const onOkay = (text) => {
          name = text;
          status = 1;
      }
  
    const showDialog = () => {
          open(
              Dialog,
              {
                  message: "What is your name?",
                  hasForm: true,
                  onCancel,
                  onOkay
              },
              {
                  closeButton: false,
              closeOnEsc: false,
              closeOnOuterClick: false,
              }
        );
      };
  </script>
  
  <section>
      <div on:click={showPopup}>
        <slot></slot>
    </div>
  
      {#if status === 1}
          <p>Hi {name}! 👋</p>
      {:else if status === -1}
          <p><em>Dialog was canceled</em></p>
      {/if}
  
      <div id="state">
          {#if opening}
              <p>opening modal...</p>
          {:else if opened}
              <p>opened modal!</p>
          {:else if closing}
              <p>closing modal...</p>
          {:else if closed}
              <p>closed modal!</p>
          {/if}
      </div>
  </section>
  
  <style>
      section {
          padding-top: 0.5em;
      }
      
      #state {
          position: absolute;
          top: 0;
          right: 0;
          opacity: 0.33;
          font-size: 0.8em;
      }
  </style>
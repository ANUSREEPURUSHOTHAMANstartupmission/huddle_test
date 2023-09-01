
<script>
    import {onMount} from 'svelte';
  
    let speaker_list = [];
  
    export let title;
    export let label;
    export let category;
  
    onMount(()=>{
      fetch(`https://events.startupmission.in/api/event/huddle-global-2023/speakers?category=${category}`)
          .then(response => response.json())
          .then((json) => {
            speaker_list = json;
          });
    });
  
  </script>
  
  
  {#each Object.entries(speaker_list) as [category, speakers]}
    <div class="mx-auto speakers__container ">
  
      <div class="grid grid-cols-1 gap-10 md:grid-cols-4 sm:grid-cols-3">
  
        <div class="mb-20 text-center flex flex-col justify-end">
          <p class="mb-3 text-5xl text-yellow-400 font-spl">{label}</p>
          <h1 class="text-5xl font-black text-huddle">{title}</h1>
        </div>
  
        {#each speakers as {name, designation, organisation, photo, linkedin}}
  
        <div class="themeholy-product product-grid relative group">
            <div class="product-img">
                <img src={photo} alt="Product Image">
                                            
                <div class="absolute bottom-0 left-0  group-hover:hidden flex items-center justify-center">
                    <p class="text-white text-lg  bg-[#212529] bg-opacity-70 p-2">{name}</p>
                </div> 
                <div class="actions flex flex-col p-2">
                    <p class="text-white text-xl font-bold ">{name}</p>
                    <p class=" text-white text-xs flex px-6">{designation}</p>
                </div>
            </div>
        </div>
        {/each}
      </div>
  
    </div>
  {/each}
  
  
  <style lang="scss">
    .speaker{
      position: relative;
      //width: 100%;
      overflow: hidden;
  
      &:hover{
        &::after{
          top: 0;
        }
  
        .content{
          top: 50%;
          p{
            visibility: visible;
          }
        }
  
        .linkedin{
          right: 20px;
        }
      }
  
      .linkedin{
        position: absolute;
        top: 20px;
        right: -30px;
        transition: all 500ms ease;
        z-index: 2;
      }
  
      .content{
        position: absolute;
        top: 78%;
        z-index: 2;
        padding: 15px 10px;
        transition: all 500ms ease;
        
        h3{
          font-size: 1.25rem;
          font-weight: bold;
          margin-bottom: .5rem;
          
  
        }
  
        p{
          font-size: .9rem;
          font-weight: 300;
          
          visibility: hidden;
          transition: all 500ms ease;
        }
      }
  
      &::after{
        position: absolute;
        content: '';
        left: 0;
        top: 75%;
        border: 15px;
        right: 0;
        bottom: 0;
        border-radius: 10px;
        background: rgba(0, 0, 0, 0.8);
        z-index: 1;
        transition: all 500ms ease
      }
    }
  </style>
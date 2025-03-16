<script lang="ts">
    import { Button } from "$lib/components/ui/button";
    import * as Card from "$lib/components/ui/card/index.js";
    import { Input } from "$lib/components/ui/input";
    let data = $state([]);
    
    const backendUrl = import.meta.env.VITE_BACKEND_URL;
    async function fetchData() {
      try {
        const response = await fetch(backendUrl);
        if (!response.ok) throw new Error('Failed to fetch data');
        data = await response.json();
        return data 
      } catch (error) {
        return error
      }
    }
  
  
    fetchData();
    let url = $state('');
  </script>
   
  
  <div class="flex flex-col items-center justify-start h-screen color-tertiary gap-10 mt-10">
          
    <div>
          <form action="{backendUrl}/add" method="post">
            <Card.Root class="color-secondary h-full">
                <Card.Header>
                    <Card.Title>Inserisci il tuo Url</Card.Title>
                    <Card.Description>Questo url sarà controllato dall'admin</Card.Description>
                </Card.Header>
                <Card.Content>
                    <Input type="url" bind:value={url}  name="url" placeholder="https://rickastley.com" class="max-w-xs" />
          </Card.Content>
          <Card.Footer class="flex justify-end">
              <Button class="color-primary" type="submit">Invia</Button>
            </Card.Footer>
        </Card.Root>
    </form>
        
    </div>
  
    <div class="w-3/4 rounded-md   relative overflow-x-auto">
      <table class="w-full text-sm text-left rtl:text-right text-gray-500">
          <thead class="text-xs text-gray-700 uppercase bg-gray-50">
              <tr>
                  <th scope="col" class="px-6 py-3">
                      Url
                  </th>
                
              </tr>
          </thead>
          <tbody>
              {#each data.urls as item}
              <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700 border-gray-200">
                <td class="px-6 py-4">
                    {item}
                </td>
              </tr>
            {/each}          
          </tbody>
      </table>
    </div>
  
    
  </div>
  
  <style>
      :global(body) {
          /* applies to <body> */
          margin: 0;
      padding: 0;
      font-family: 'Inter', sans-serif;
      background-color: #14213D;
      }
    :global(.color-tertiary) {
      background-color: #14213D;
    }
    :global(.color-primary) {
      background-color: #FCA311;
    }
    :global(.color-secondary) {
      background-color: #E5E5E5;
    }
  
      div :global(strong) {
          /* applies to all <strong> elements, in any component,
             that are inside <div> elements belonging
             to this component */
          color: goldenrod;
      }
  </style>
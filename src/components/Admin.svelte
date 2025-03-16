<script lang="ts">
    import { Button } from "$lib/components/ui/button";
    import * as Card from "$lib/components/ui/card/index.js";
    import { Input } from "$lib/components/ui/input";
    let data = $state([]);
  
    const backendUrl = import.meta.env.VITE_BACKEND_URL;

    async function fetchData() {
      try {
        const response = await fetch(backendUrl+'/admin');
        if (!response.ok) throw new Error('Failed to fetch data');
        data = await response.json();
        return data 
      } catch (error) {
        return error
      }
    }   

    fetchData();
  </script>
   
<div class="flex flex-col items-center justify-center h-screen color-tertiary gap-10 mt-10">

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
                  <td class="px-6 py-4 flex gap-16 justify-start ">
                      {item}
                      <form action="{backendUrl}/admin/accept" method="post" class="flex gap-4">
                        <Input type="hidden" value={item}  name="url" />
                        <Input type="text" name="password" class="min-w-32"/>
                        <Button type="submit" class="color-primary">Accept</Button>
                    </form> 
                  </td>
            </tr>
          {/each}          
        </tbody>
    </table>
  </div>
</div>
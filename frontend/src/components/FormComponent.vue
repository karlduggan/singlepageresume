<template>
 <div class="">
    <form  class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4 divide-y-2 divide-solid divide-gray-100 flex flex-col space-y-4">
        <!--Name and Contact-->
        <div class="mb-5">
            <div class="flex mb-4 gap-4 w-full">
                <div class="w-full">
                    <label class="block text-gray-400 font-bold text-left text-sm" for="name">
                    First Name
                    </label>
                    <input  class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="text" placeholder="John">
                </div>
                <div class="w-full">
                    <label class="block text-gray-400 font-bold text-left text-sm" for="name">
                    Last Name
                    </label>
                    <input  class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="text" placeholder="Doe">
                </div>

            </div>
            <div class="">
                <div class="mb-4">
                    <label class="block text-gray-400 font-bold text-left text-sm" for="name">
                    Telephone
                    </label>
                    <input  class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="tel" placeholder="Telephone">
                </div>
                <div class="mb-4">
                    <label class="block text-gray-400 font-bold text-left text-sm" for="name">
                    Email
                    </label>
                    <input  class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="email" placeholder="Email">
                </div>
                <div class="">
                    <label class="block text-gray-400 font-bold text-left text-sm" for="name">
                    Website or Github
                    </label>
                    <input  class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="tel" placeholder="URL">
                </div>
              
            </div>
        </div>
        <!-- Address -->
        <div class="">
            <div class="mb-4 mt-4">
                <div class="mb-4">
                    <label class="block text-gray-400 font-bold text-left text-sm" for="name">
                    Address
                    </label>
                    <input  class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="text" placeholder="Address Line 1">
                </div>
                <div class="mb-4">
                    <input  class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="text" placeholder=" Address Line 2">
                </div>
                <div class="flex mb-4 gap-4 w-full">
                <div class="w-full">
                    <input  class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="text" placeholder="City">
                </div>
                <div class="w-full">
                    <input  class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="text" placeholder="Postcode">
                </div>

            </div>
           
              
            </div>
        </div>
        <!-- Profile Summary -->
        <div>
            <div class="mt-4 mb-4">
                <div class="mb-4">
                    <label class="block text-gray-400 font-bold text-left text-sm" for="name">
                    Profile Summary
                    </label>
                    <textarea  class="shadow h-28 appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="tel" placeholder="Summary..."></textarea>
                </div>
            </div>

        </div>
      
      
    </form>
  </div>

</template>

<script>
export default {
    name: "FormComponent",
    data(){
        
    }

}
</script>

<style scoped>

</style>
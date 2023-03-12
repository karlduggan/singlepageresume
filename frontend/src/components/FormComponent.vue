<template>
 <div class="">
        <ModalComponent :open="modalOpen">
            <div>
                <h1 class="block text-gray-600 font-bold text-left text-lg">{{ modalName }} Section</h1>
            </div>
            <div v-for="(name, index) in modalItems" :key="index" class="flex justify-center gap-4 p-4 items-center border-b-2">
                    <div>
                        <p>{{ index + 1 }}</p>
                    </div>
                    <div>
                        <input v-on:input="updateItem(index, $event)" :value="name" class=" appearance-none border-none w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
                    </div>
                    <div class="cursor-pointer" @click="deleteItem(index)">
                        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="red-700"><line x1="18" y1="6" x2="6" y2="18"></line><line x1="6" y1="6" x2="18" y2="18"></line></svg>
                    </div>
            </div>
            <div class="flex justify-center gap-4 mt-5">
                <a class="cursor-pointer bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded" @click="modalOpen = false">
                    Close
                </a>
            </div>
        </ModalComponent>
        <!--Edit Modal-->
        <ModalComponent :open="editModalOpen">
            <div>
                <h1 class="block text-gray-600 font-bold text-left text-lg">{{ modalName }} Section</h1>
            </div>
            <div v-for="(item, index) in modalItems" :key="index" class="flex justify-center gap-4 p-4 items-center border-b-2">
                   
                        <p>{{ index + 1 }}</p>
                        <input v-on:input="updateItem2(index, $event, 'title')" :value="item.title" class=" appearance-none border-none w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
                    
                    
                        <textarea v-on:input="updateItem2(index, $event, 'text')" :value="item.text" class="mt-4 shadow h-28 appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="tel" ></textarea>
                   
                    <div class="cursor-pointer" @click="deleteItem2(index)">
                        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="red-700"><line x1="18" y1="6" x2="6" y2="18"></line><line x1="6" y1="6" x2="18" y2="18"></line></svg>
                    </div>

            </div>
            <div class="flex justify-center gap-4 mt-5">
                <a class="cursor-pointer bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded" @click="editModalOpen = false">
                    Close
                </a>
            </div>
        </ModalComponent>
    <form  class="bg-white shadow-md rounded px-8 pt-6 pb-8 flex flex-col space-y-4">
        <h1 class="text-2xl font-bold text-gray-600">Single Page Resume</h1>
        <div class="flex justify-between gap-4">
            <a class="cursor-pointer bg-emerald-500 w-[100%] hover:bg-emerald-600 text-white font-bold text-xs py-2 px-4 rounded" @click="loadJSON">Load JSON</a>
            <a class="cursor-pointer bg-yellow-500 w-[100%] hover:bg-yellow-600 text-white font-bold text-xs py-2 px-4 rounded" @click="saveJSON">Save JSON</a>
        </div>
        <!--Name and Contact-->
        <div class="mb-5">
            <div class="flex mb-4 gap-4 w-full">
                <div class="w-full">
                    <label class="block text-gray-600 font-bold text-left text-sm" for="name">
                    First Name
                    </label>
                    <input  v-model="cv_data.firstname" class="shadow appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="text" placeholder="John" maxlength="12">
                </div>
                <div class="w-full">
                    <label class="block text-gray-600 font-bold text-left text-sm" for="name">
                    Last Name
                    </label>
                    <input  v-model="cv_data.lastname" class="shadow appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="text" placeholder="Doe"  maxlength="12">
                </div>

            </div>
            <div class="">
                <div class="mb-4">
                    <label class="block text-gray-600 font-bold text-left text-sm" for="name">
                    Telephone
                    </label>
                    <input v-model="cv_data.telephone"  class="shadow appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="tel" placeholder="Telephone">
                </div>
                <div class="mb-4">
                    <label class="block text-gray-600 font-bold text-left text-sm" for="name">
                    Email
                    </label>
                    <input v-model="cv_data.email" class="shadow appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="email" placeholder="Email">
                </div>
                <div class="">
                    <label class="block text-gray-600 font-bold text-left text-sm" for="name">
                    Website or Github
                    </label>
                    <input v-model="cv_data.link1" class="shadow appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="tel" placeholder="URL">
                </div>
              
            </div>
        </div>
        <!-- Address -->
        <div class="">
            <div class="mb-4 mt-4">
                <div class="mb-4">
                    <label class="block text-gray-600 font-bold text-left text-sm" for="name">
                    Address
                    </label>
                    <input  v-model="cv_data.addressline1" class="shadow appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="text" placeholder="Address Line 1">
                </div>
                <div class="mb-4">
                    <input v-model="cv_data.addressline2" class="shadow appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="text" placeholder=" Address Line 2">
                </div>
                <div class="flex mb-4 gap-4 w-full">
                <div class="w-full">
                    <input v-model="cv_data.city" class="shadow appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="text" placeholder="City">
                </div>
                <div class="w-full">
                    <input v-model="cv_data.postcode" class="shadow appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="text" placeholder="Postcode">
                </div>

            </div>
           
              
            </div>
        </div>
        <!-- Profile Summary -->
        <div>
            <div class="mt-4 mb-4">
                <div class="mb-4">
                    <label class="block text-gray-600 font-bold text-left text-sm" for="name">
                    Profile Summary
                    </label>
                    <textarea v-model="cv_data.profilesummary" :maxlength="summaryMaxCount" class="shadow h-28 appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="tel" placeholder="Summary..."></textarea>
                    <p class="text-left text-xs ext-gray-600 ">Characters left: {{ summaryMaxCount - summaryCount }}</p>
                </div>
            </div>
        </div>
        <!-- Skills -->
        <div>
            <div class="mt-4 ">
                <div class="mb-4">
                    <label class="block text-gray-600 font-bold text-left text-sm" for="name">
                    Skills
                    </label>
                    <div class="flex">
                        <input v-model="skillsValue"  v-on:keyup.enter="addToList('skills')" maxlength="100" class="shadow appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="tel" placeholder="Press enter to add value">
                        <p class="pl-4 py-2 text-gray-400 cursor-pointer" @click="openModal('list01')">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1" stroke-linecap="round" stroke-linejoin="round" class="feather feather-edit"><path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"></path><path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"></path></svg>
                        </p>
                    </div>
                    <p class="p-1 text-left text-gray-400 text-xs">{{ cv_data.lists.list01.items.length}} out of {{ maxEntries }}</p>
                </div>
            </div>
            
        </div>
        <!-- Languages -->
        <div>
            <div class="mt-4 ">
                <div class="mb-4">
                    <label class="block text-gray-600 font-bold text-left text-sm" for="name">
                    Languages
                    </label>
                    <div class="flex">
                        <input v-model="languageValue"  v-on:keyup.enter="addToList('languages')" maxlength="100"  class="shadow appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="tel" placeholder="Press enter to add value">
                        <p class="pl-4 py-2 text-gray-400 cursor-pointer" @click="openModal('list02')">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1" stroke-linecap="round" stroke-linejoin="round" class="feather feather-edit"><path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"></path><path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"></path></svg>
                        </p>
                    </div>
                    <p class="p-1 text-left text-gray-400 text-xs">{{ cv_data.lists.list02.items.length}} out of {{ maxEntries }}</p>
                </div>
            </div>
        </div>
        <!-- Frameworks -->
        <div>
            <div class="mt-4 ">
                <div class="mb-4">
                    <label class="block text-gray-600 font-bold text-left text-sm" for="name">
                    Frameworks
                    </label>
                    <div class="flex">
                        <input v-model="frameworkValue" v-on:keyup.enter="addToList('frameworks')" maxlength="100"  class="shadow appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="tel" placeholder="Press enter to add value">
                        <p class="pl-4 py-2 text-gray-400 cursor-pointer" @click="openModal('list03')">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1" stroke-linecap="round" stroke-linejoin="round" class="feather feather-edit"><path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"></path><path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"></path></svg>
                        </p>
                    </div>
                    <p class="p-1 text-left text-gray-400 text-xs">{{ cv_data.lists.list03.items.length}} out of {{ maxEntries }}</p>
                </div>
            </div>
        </div>
        <!-- Work Experience -->
        <div>
            <div class="mt-4">
                <label class="block text-gray-600 font-bold text-left text-sm" for="name">
                    Experience
                </label>
                <div class="flex">
                    <input v-model="experience_title" maxlength="100" class="shadow appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="tel" placeholder="Job Title">
                </div>
                <textarea v-model="experience_text" class="mt-4 shadow h-28 appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="tel" placeholder="Job description"></textarea>
            </div>
            <div class="mt-2 flex justify-between gap-4">
                <a class="cursor-pointer bg-blue-500 w-[100%] hover:bg-blue-600 text-white font-bold py-2 px-4 rounded text-sm " @click="addToList('experience')" >Add</a>
                <p class="cursor-pointer bg-emerald-500 w-[100%] hover:bg-emerald-600 text-white font-bold py-2 px-4 rounded text-sm" @click="openModal('experience')">Edit</p>
                <div class="w-[100%] self-center">
                    <p class="text-gray-400 text-xs">0 out of 3</p>
                </div>
            </div>
        </div>
        <!-- Education and Certifications -->
        <div>
            <div class="mt-4">
                <label class="block text-gray-600 font-bold text-left text-sm" for="name">
                    Education & Certifications
                </label>
                <div class="flex">
                    <input v-model="education_title" maxlength="100" class="shadow appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="tel" placeholder="Education Title">
                </div>
                <textarea v-model="education_text" class="mt-4 shadow h-28 appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="tel" placeholder="Education description"></textarea>
            </div>
            <div class="mt-2 flex justify-between gap-4">
                <a class="cursor-pointer bg-blue-500 w-[100%] hover:bg-blue-600 text-white font-bold py-2 px-4 rounded text-sm " @click="addToList('education')" >Add</a>
                <p class="cursor-pointer bg-emerald-500 w-[100%] hover:bg-emerald-600 text-white font-bold py-2 px-4 rounded text-sm" @click="openModal('education')">Edit</p>
                <div class="w-[100%] self-center">
                    <p class="text-gray-400 text-xs">0 out of 3</p>
                </div>
            </div>
        </div>
        <!-- Projects -->
        <div>
            <div class="mt-4">
                <label class="block text-gray-600 font-bold text-left text-sm" for="name">
                    Projects
                </label>
                <div class="flex">
                    <input v-model="project_title" maxlength="100" class="shadow appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="tel" placeholder="Project Title">
                </div>
                <textarea v-model="project_text" class="mt-4 shadow h-28 appearance-none border border-gray-300 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" id="name" type="tel" placeholder="Project description"></textarea>
            
            </div>
            <div class="mt-2 flex justify-between gap-4">
                <a class="cursor-pointer bg-blue-500 w-[100%] hover:bg-blue-600 text-white font-bold py-2 px-4 rounded text-sm " @click="addToList('project')" >Add</a>
                <p class="cursor-pointer bg-emerald-500 w-[100%] hover:bg-emerald-600 text-white font-bold py-2 px-4 rounded text-sm" @click="openModal('project')">Edit</p>
                <div class="w-[100%] self-center">
                    <p class="text-gray-400 text-xs">0 out of 3</p>
                </div>
            </div>
            
        </div>
            <a class="cursor-pointer bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" @click="emit_download_pdf">Download PDF</a>
            <p class="text-gray-600 text-xs">Created by Karl Duggan 2023</p>
    </form>
  </div>

</template>

<script>
import ModalComponent from '../components/ModalComponent.vue';
export default {
    name: "FormComponent",
    components: {
        ModalComponent
    },
    setup(){
        //const data = JSON.parse(localStorage.getItem('dataCV'));
         //Or use sessionStorage if you saved data there
        //if (data) {
        //this.cv_data = Object.assign(this.cv_data, data);
        //}
    },
    watch : {
        'cv_data.firstname' : function(){
            this.emit_cv_data()
            this.updateLocalStorage()
        },
        'cv_data.lastname' : function(){
            this.emit_cv_data()
            this.updateLocalStorage()
        },
        'cv_data.telephone' : function(){
            this.emit_cv_data()
            this.updateLocalStorage()
        },
        'cv_data.email' : function(){
            this.emit_cv_data()
            this.updateLocalStorage()
        },
        'cv_data.link1' : function(){
            this.emit_cv_data()
            this.updateLocalStorage()
        },
        'cv_data.addressline1' : function(){
            this.emit_cv_data()
            this.updateLocalStorage()
        },
        'cv_data.addressline2' : function(){
            this.emit_cv_data()
            this.updateLocalStorage()
        },
        'cv_data.city' : function(){
            this.emit_cv_data()
            this.updateLocalStorage()
        },
         'cv_data.postcode' : function(){
            this.emit_cv_data()
            this.updateLocalStorage()
        },
        'skillsValue' : function(){
            this.emit_cv_data()
            this.updateLocalStorage()
        },
        'languageValue' : function(){
            this.emit_cv_data()
            this.updateLocalStorage()
        },
        'frameworkValue' : function(){
            this.emit_cv_data()
            this.updateLocalStorage()
        },
        'cv_data.profilesummary' : function(){
            this.emit_cv_data()
            this.countCharacters()
            // Observe word count
            this.updateSummaryLayout()
            this.updateLocalStorage()
        },
        deep: true
    },
    data(){
        return {
            // Edit Modal for (Experience, Education and Projects)
            editModalOpen: false,
            // Modal state
            modalOpen: false,
            modalSelection : null,
            modalName: "None",
            modalSet: null,
            modalItems: [],
            newValue: "",
            // Character Counter
            summaryMaxCount : 625,
            summaryCount: 0,
            summaryWordLineCount: 0,
            summaryCharacterLineCount: 0,
            // Skills Value
            skillsValue: "",
            // Languages Value 
            languageValue: "",
            // Framework Value
            frameworkValue: "",
            // Experience
            experience_title: "",
            experience_text: "",
            // Education 
            education_title: "",
            education_text: "",
            // Project
            project_title: "",
            project_text: "",
            // Max entries for lists
            maxEntries : 5,
            cv_data : {
                firstname : "",
                lastname : "",
                telephone : "",
                email : "",
                link1 : "",
                addressline1 : "",
                addressline2 : "",
                city : "",
                postcode : "",
                profilesummary : "",
                // Bullet point list used for
                lists: {
                    list01: {
                        // Skills
                        set: "list01",
                        name: "Skills",
                        items : []
                        },
                    list02: {
                        // Languages
                        set: "list02",
                        name: "Languages",
                        items : []
                    },
                    list03: {
                        // Frameworks
                        set: "list03",
                        name: "Frameworks",
                        items : []
                    }
                },
                experience: {
                    name: "Experience",
                    set: "experience",
                    display: false,
                    items: []
                },
                education: {
                    name: "Education",
                    set: "education",
                    display: false,
                    items: []
                },
                project: {
                    name: "Projects",
                    set: "project",
                    display: false,
                    items: []
                }
            }
        }
    },
    methods:{
        updateLocalStorage(){
            // Set data to localStorage
            localStorage.setItem('dataCV', JSON.stringify(this.cv_data));
        },
        clearLocalStorage() {
            localStorage.clear();
        },
        saveJSON(){
            let jsonData = this.cv_data
            const blobData = new Blob([JSON.stringify(jsonData, null, 2)], { type: 'application/json' });
            const downloadLink = document.createElement('a');
            downloadLink.download =  "Saved_CV_Data";
            downloadLink.href = URL.createObjectURL(blobData);
            downloadLink.onclick = () => {
                setTimeout(() => {
                URL.revokeObjectURL(downloadLink.href);
                }, 1500);
                };
            downloadLink.click();
                
        },
        loadJSON(){
            // Create an input element of type "file"
            const input = document.createElement('input');
            input.type = 'file';

            // Define a function to handle the file selection
            input.onchange = () => {
                const file = input.files[0];
                const reader = new FileReader();

                // Define a function to handle the file load
                reader.onload = (e) => {
                const fileContent = e.target.result;
                const cvData = JSON.parse(fileContent);
                this.cv_data = cvData; // Assign the JSON object to this.cv_data
                };

                // Read the selected file as text
                reader.readAsText(file);
            };
            // Click the input element to trigger the file selector dialog
            input.click();
        },
        updateItem(index, event){
            const updateValue = event.target.value
            this.cv_data.lists[this.modalSet].items[index] = updateValue
            this.emit_cv_data()
            this.updateLocalStorage()
        },
        updateItem2(index, event, type){
            const updateValue = event.target.value
            this.cv_data[this.modalSet].items[index][type] = updateValue
            this.emit_cv_data()
            this.updateLocalStorage()
        },
        deleteItem(index){
            // Get the currect list from modalSelected
            this.cv_data.lists[this.modalSet].items.splice(index, 1)
            this.emit_cv_data()
            this.updateLocalStorage()
        },
        deleteItem2(index){
            this.cv_data[this.modalSet].items.splice(index, 1)
            this.emit_cv_data()
        },

        // Edit Modal 
        openModal(option){
            // Set up the selected modal from the option chosen
            let openModal1 = false;
            let openModal2 = false;
            switch(option) {
                case "list01":
                    //Skills
                    if(this.cv_data.lists.list01.items.length > 0){
                        this.modalItems = this.cv_data.lists.list01.items;
                        this.modalName = this.cv_data.lists.list01.name;
                        this.modalSet = this.cv_data.lists.list01.set;
                        openModal1 = true; 
                    }
                    break;
                case "list02":
                    //Languages
                    if(this.cv_data.lists.list02.items.length > 0){
                        this.modalItems = this.cv_data.lists.list02.items;
                        this.modalName = this.cv_data.lists.list02.name;
                        this.modalSet = this.cv_data.lists.list02.set;
                        openModal1 = true;
                    }
                    break;
                case "list03":
                    //Frameworks
                    if(this.cv_data.lists.list03.items.length > 0){
                        this.modalItems = this.cv_data.lists.list03.items
                        this.modalName = this.cv_data.lists.list03.name;
                        this.modalSet = this.cv_data.lists.list03.set;
                        openModal1 = true;
                    }
                    break;
                case "experience":
                //Frameworks
                if(this.cv_data.experience.items.length > 0){
                    this.modalItems = this.cv_data.experience.items
                    this.modalName = this.cv_data.experience.name;
                    this.modalSet = this.cv_data.experience.set;
                    openModal2 = true;
                }
                break;
                case "education":
                //Frameworks
                if(this.cv_data.education.items.length > 0){
                    this.modalItems = this.cv_data.education.items
                    this.modalName = this.cv_data.education.name;
                    this.modalSet = this.cv_data.education.set;
                    openModal2 = true;
                }
                break;
                case "project":
                //Frameworks
                if(this.cv_data.project.items.length > 0){
                    this.modalItems = this.cv_data.project.items
                    this.modalName = this.cv_data.project.name;
                    this.modalSet = this.cv_data.project.set;
                    openModal2 = true;
                }
                break;
               
            }
            this.modalOpen = openModal1
            this.editModalOpen = openModal2
            
        },
        countCharacters(){
            console.log('count')
            this.summaryCount = this.cv_data.profilesummary.length
        },
        countWordsPerLine(){
            const maxNumberOfCharactersPerLine = 10;
            
            // Split text into lines array
            let lines = this.cv_data.profilesummary.split('\n');
            // Get the last and current line array
            let words = lines.at(-1).split(' ');
            // Assign current word count
            this.summaryWordLineCount = words.length
            // Check if word count is greater or equal to max word count
            if(this.summaryCharacterLineCount > maxNumberOfCharactersPerLine ){
                // get the second last word and add a \n line break
                this.cv_data.profilesummary.split(' ').at(-2)  
                console.log(this.cv_data.profilesummary.split(' ').at(-2))
                this.summaryCharacterLineCount = 0
            }
        },
        handleInput() {
            let maxRows = 6;
            let maxChars = 10;
            let lines = this.cv_data.profilesummary.split("\n");
            let newLines = [];

      for (let i = 0; i < lines.length; i++) {
        let line = lines[i];
        let lineStart = 0;
        while (line.length > maxChars) {
          let lastSpace = line.lastIndexOf(" ", lineStart + maxChars);
          let newLine = line.substring(lineStart, lastSpace);
          newLines.push(newLine);
          lineStart = lastSpace + 1;
          line = line.substring(lineStart);
        }
        newLines.push(line);
        if (newLines.length >= maxRows) break;
      }
      this.cv_data.profilesummary = newLines.join("\n");
    },
    updateSummaryLayout(){
        let maxRows = 7;
        let maxChars = 90;
        let lines = this.cv_data.profilesummary.split("\n");
        let newLines = [];
        
            for (let i = 0; i < lines.length; i++) {
                console.log(i)
                let line = lines[i];
                let lineStart = 0;
                while (line.length > maxChars) {
                    console.log("testing infinte")
                    let lastSpace = line.lastIndexOf(" ", lineStart + maxChars);
                    if (lastSpace === -1) {
                        lastSpace = lineStart + maxChars;
                    }
                    let newLine = line.substring(lineStart, lastSpace);
                    newLines.push(newLine);
                    lineStart = lastSpace + 1;
                    line = line.substring(lineStart);
                    }
                    newLines.push(line);
                    if (newLines.length >= maxRows) break;
                }
            this.cv_data.profilesummary = newLines.join("\n");
            this.updateLocalStorage()
        
        },
        addToList : function (listName){
           
            let selectedList;
            let value;
            let textarea;
            let pushObject = false;
            switch(listName){
                case "skills":
                    selectedList = this.cv_data.lists.list01.items;
                    value = this.skillsValue;
                    // Clear Entry
                    this.skillsValue = ""
                    break;
                case "languages":
                    selectedList = this.cv_data.lists.list02.items;
                    value = this.languageValue;
                    // Clear Entry
                    this.languageValue = ""
                    break;
                case "frameworks":
                    selectedList = this.cv_data.lists.list03.items
                    value = this.frameworkValue;
                    // Clear Entry
                    this.frameworkValue = ""
                    break;
                case "experience":
                    selectedList = this.cv_data.experience.items
                    value = this.experience_title;
                    textarea = this.experience_text
                    pushObject = true;
                    // Clear Entry
                    this.experience_title = ""
                    this.experience_text = ""
                    break;
                case "education":
                    selectedList = this.cv_data.education.items
                    value = this.education_title;
                    textarea = this.education_text
                    pushObject = true;
                    // Clear Entry
                    this.education_title = ""
                    this.education_text = ""
                    break;
                case "project":
                    selectedList = this.cv_data.project.items
                    value = this.project_title;
                    textarea = this.project_text
                    pushObject = true;
                    // Clear Entry
                    this.project_title = ""
                    this.project_text = ""
                    break
            }
            // Check if entry is an object push or a string value push
            if(pushObject){
                let newObject = {'title': value, 'text': textarea}
                selectedList.push(newObject)
            }else {
                // Check if max value has already been reached, if not then input data
                if(selectedList.length < this.maxEntries){
                    // Add data to selected list
                    selectedList.push(value)
                } else {
                    // Give error message in input field
                    switch(listName){
                    case "skills":
                        this.skillsValue = "Max entry of " + this.maxEntries + " reached!"
                        break;
                    case "languages":
                        this.languageValue = "Max entry of " + this.maxEntries + " reached!"
                        break;
                    case "frameworks":
                        this.frameworkValue = "Max entry of " + this.maxEntries + " reached!"
                        break;
                    }
                }
            }
            this.updateLocalStorage()
            this.emit_cv_data()
        },

        emit_cv_data : function(){
            this.$emit('cv-data-emitted',this.cv_data)
            
        },
        emit_download_pdf : function(){
            this.$emit('download-pdf-emitted')
        }
    }
}
</script>

<style scoped>

</style>
<template>

    <div class="progressbar mb-5 mx-5"  v-if="!isValidate">
        <div class="progress-indicator" :style="{width: `${widthIndicator}%`}"></div>
        <div class="progress-step" :class="{'active': step <= 3}" data-title="Full Name"></div>
        <div class="progress-step" :class="{'active': step === 2 || step === 3}" data-title="Info"></div>
        <div class="progress-step" :class="{'active': step === 3}" data-title="More Info"></div>
    </div>

    <div class="card" v-if="!isValidate">
        <form method="post" @submit.prevent="handleSubmit">
            <div class="card-header bg-white">
                <h4 class="card-title">Multistep Form Vue JS</h4>
            </div>

            <div class="card-body">

                <!-- Step 1 -->
                <div v-show="step === 1" class="form-step"> 
                    <div class="mb-3">
                        <label class="col-form-label fw-bold">First Name</label>
                        <input type="text" class="form-control" placeholder="Enter first name..." v-model="stateFormOne.firstName">
                        <div v-if="v$One.firstName.$errors.length > 0" class="text-danger mt-1">
                            {{ v$One.firstName.$errors[0].$message }}
                        </div> 
                    </div>
                    <div class="mb-3">
                        <label class="col-form-label fw-bold">Last Name</label>
                        <input type="text" class="form-control" placeholder="Enter last name..." v-model="stateFormOne.lastName">
                        <div v-if="v$One.lastName.$errors.length > 0" class="text-danger mt-1">
                            {{ v$One.lastName.$errors[0].$message }}
                        </div> 
                    </div>
                </div>

                <!-- Step 2 -->
                <div v-show="step === 2" class="form-step"> 
                    <div class="mb-3">
                        <label class="col-form-label fw-bold">Address</label>
                        <input type="text" class="form-control" placeholder="Enter address..." v-model="stateFormTwo.address">
                        <div v-if="v$Two.address.$errors.length > 0" class="text-danger mt-1">
                            {{ v$Two.address.$errors[0].$message }}
                        </div> 
                    </div>
                    <div class="mb-3">
                        <label class="col-form-label fw-bold">Phone Number</label>
                        <input type="text" class="form-control" placeholder="Enter phone number..." v-model="stateFormTwo.phoneNumber">
                        <div v-if="v$Two.phoneNumber.$errors.length > 0" class="text-danger mt-1">
                            {{ v$Two.phoneNumber.$errors[0].$message }}
                        </div> 
                    </div>
                </div>

                <!-- Step 3 -->
                <div v-show="step === 3" class="form-step"> 
                    <div class="mb-3">
                        <label class="col-form-label fw-bold">Your Favorite Character</label>
                        <div>
                            <div class="form-check">
                                <input class="form-check-input" type="checkbox" value="Naruto" id="naruto" v-model="stateFormThree.favoriteCharacter">
                                <label class="form-check-label" for="naruto">
                                    Naruto
                                </label>
                            </div>
                            <div class="form-check">
                                <input class="form-check-input" type="checkbox" value="Sasuke" id="sasuke" v-model="stateFormThree.favoriteCharacter">
                                <label class="form-check-label" for="sasuke">
                                    Sasuke
                                </label>
                            </div>
                            <div class="form-check">
                                <input class="form-check-input" type="checkbox" value="Sakura" id="sakura" v-model="stateFormThree.favoriteCharacter">
                                <label class="form-check-label" for="sakura">
                                    Sakura
                                </label>
                            </div>
                            <div class="form-check">
                                <input class="form-check-input" type="checkbox" value="Jiraiya" id="jiraiya" v-model="stateFormThree.favoriteCharacter">
                                <label class="form-check-label" for="jiraiya">
                                    Jiraiya
                                </label>
                            </div>
                            <div class="form-check">
                                <input class="form-check-input" type="checkbox" value="Orochimaru" id="orochimaru" v-model="stateFormThree.favoriteCharacter">
                                <label class="form-check-label" for="orochimaru">
                                    Orochimaru
                                </label>
                            </div>
                            <div class="form-check">
                                <input class="form-check-input" type="checkbox" value="Tsunade" id="tsunade" v-model="stateFormThree.favoriteCharacter">
                                <label class="form-check-label" for="tsunade">
                                    Tsunade
                                </label>
                            </div>
                        </div>
                        <div v-if="v$Three.favoriteCharacter.$errors.length > 0" class="text-danger mt-1">
                            {{ v$Three.favoriteCharacter.$errors[0].$message }}
                        </div> 
                    </div>
                </div>
                
            </div>

            <div class="card-footer d-flex bg-white" :class="[step === 1 ? 'justify-content-end' : 'justify-content-between']">
                <button type="button" class="btn btn-primary" v-show="step !== 1" @click="back">Back</button>
                <button type="button" class="btn btn-primary" v-show="step !== 3" @click="next">Next</button>
                <button type="submit" class="btn btn-primary" v-show="step === 3">Submit</button>
            </div>

        </form>

    </div>
    <div v-else>
        <div class="alert alert-success">
            Successfully created data
        </div>
    </div>
    
    <div v-if="isValidate" class="mt-5 mb-5 pb-5">
        <div class="card">
            <div class="card-header">
                <h4 class="card-title mb-0">Your Data : </h4>
            </div>
            <div class="card-body">
                <table>
                    <tr>
                        <td class="pb-2 align-top">First Name</td>
                        <td class="ps-3 pe-1 align-top">:</td>
                        <td class="align-top">{{ stateFormOne.firstName }}</td>
                    </tr>
                    <tr>
                        <td class="pb-2 align-top">Last Name</td>
                        <td class="ps-3 pe-1 align-top">:</td>
                        <td class="align-top">{{ stateFormOne.lastName }}</td>
                    </tr>
                    <tr>
                        <td class="pb-2 align-top">Address</td>
                        <td class="ps-3 pe-1 align-top">:</td>
                        <td class="align-top">{{ stateFormTwo.address }}</td>
                    </tr>
                    <tr>
                        <td class="pb-2 align-top">Phone Number</td>
                        <td class="ps-3 pe-1 align-top">:</td>
                        <td class="align-top">{{ stateFormTwo.phoneNumber }}</td>
                    </tr>
                    <tr>
                        <td class="pb-2 align-top">Favorite Character</td>
                        <td class="ps-3 pe-1 align-top">:</td>
                        <td class="align-top">
                            <ul class="ps-4">
                                <li v-for="character in stateFormThree.favoriteCharacter" :key="character">
                                    {{character}}
                                </li>
                            </ul>
                        </td>
                    </tr>
                </table>

                <div class="text-center mt-5 mb-3">
                    <button type="button" class="btn btn-danger" @click="createAgain">Create Again</button>
                </div>
            </div>
        </div>
        
    </div>

</template>

<script setup>
import { ref } from 'vue';
import useVuelidate from '@vuelidate/core';
import { required, minLength, maxLength, numeric, helpers } from '@vuelidate/validators';

const step = ref(1);
const isValidate = ref(false);
const widthIndicator = ref(0);

// Form Step 1 
const stateFormOne = ref({
    firstName: '',
    lastName: ''  
});
const rulesFormOne = {
    firstName: {
        required: helpers.withMessage('First name is required', required),
        $autoDirty: true,
    },
    lastName: {
        required: helpers.withMessage('Last name is required', required),
        minLength: helpers.withMessage(({ $params }) => `Last name minimum ${$params.min} charcater`, minLength(3)),
        $autoDirty: true,
    }
}
const v$One = useVuelidate(rulesFormOne, stateFormOne);

// Form Step 2 
const stateFormTwo = ref({
    address: '',
    phoneNumber: ''  
});
const rulesFormTwo = {
    address: {
        required: helpers.withMessage('Address is required', required),
        $autoDirty: true,
    },
    phoneNumber: {
        required: helpers.withMessage('Phone number is required', required),
        numeric: helpers.withMessage('Phone number must be numeric', numeric),
        minLength: helpers.withMessage(({ $params }) => `Phone number minimum ${$params.min} charcater`, minLength(9)),
        maxLength: helpers.withMessage(({ $params }) => `Phone number maximum ${$params.max} charcater`, maxLength(13)),
        $autoDirty: true,
    }
}
const v$Two = useVuelidate(rulesFormTwo, stateFormTwo);

// Form Step 3
const stateFormThree = ref({
    favoriteCharacter: [] 
});
const rulesFormThree = {
    favoriteCharacter: {
        required: helpers.withMessage('Please choose your favorice character', required),
        $autoDirty: true,
    }
}
const v$Three = useVuelidate(rulesFormThree, stateFormThree);


const back = () => {
    if(step.value !== 1) {
        step.value--;
        widthIndicator.value = 100 / (3 - (step.value - 1));
    }
    if(step.value === 1) {
        widthIndicator.value = 0;
    }
}

const next = () => {
    if(step.value === 1) {
        v$One.value.$touch(); 
        // cek jika step pertama gagal
        if(v$One.value.$invalid) return;
        step.value++;
    } else if (step.value === 2) {
        v$Two.value.$touch(); 

        // cek jika step kedua gagal
        if(v$Two.value.$invalid) return;
        step.value++;

    } else {
        v$Three.value.$touch(); 

        // cek jika step kedua gagal
        if(v$Three.value.$invalid) return;
    }
    widthIndicator.value = 100 / (3 - (step.value - 1));
}

const handleSubmit = () => {
    v$Three.value.$touch(); 
    // cek jika step ketiga gagal
    if(v$Three.value.$invalid) return;

    isValidate.value = true;
}

const createAgain = () => {
    // reset form one 
    stateFormOne.value.firstName = '';
    stateFormOne.value.lastName = '';
    stateFormTwo.value.address = '';
    stateFormTwo.value.phoneNumber = '';
    stateFormThree.value.favoriteCharacter = [];

    step.value = 1;
    isValidate.value = false;
    widthIndicator.value = 0;

    // clear message dan reset
    v$One.value.$reset(); 
    v$Two.value.$reset(); 
    v$Three.value.$reset(); 
}
</script>

<style>
/* Progressbar */
.progressbar {
  position: relative;
  display: flex;
  justify-content: space-between;
  counter-reset: step;
  margin: 2rem 0 4rem;
}

.progressbar::before,
.progress-indicator {
  content: "";
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  height: 4px;
  width: 100%;
  background-color: #dcdcdc;
  z-index: -1;
}

.progress-indicator {
  background-color: #0b5ed7;
  width: 0%;
  transition: 0.3s;
}

.progress-step {
  width: 2.1875rem;
  height: 2.1875rem;
  background-color: #dcdcdc;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.progress-step::before {
  counter-increment: step;
  content: counter(step);
}

.progress-step::after {
  content: attr(data-title);
  position: absolute;
  top: calc(100% + 0.5rem);
  font-size: 0.85rem;
  color: #666;
  white-space: nowrap;
}

.progress-step.active {
  background-color: #0b5ed7;
  color: #f3f3f3;
}
.progress-step.active::after {
  color: #0b5ed7;
}

.form-step {
    transform-origin: top;
    animation: animate 0.5s;
}

</style>
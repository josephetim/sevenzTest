<template>
    <div id="backboard" class="d-flex gap-3">
       
        <SideNav />
        <div id="main" class="mt-5 mb-5">
            <p class="avenir-normal-900 header1-purple">Update Patient Medical Record</p>
            <p class="sub-text-grey">Click the tabs to view and edit patient medical details</p>
            <div id="form-checkbox" class="mt-2 mt-md-5 pl-md-5 pl-2 pt-2 pt-md-5 pr-md-5 pr-2 pb-5">
                <CheckBoxGroup :imaging-data="investigations"  @selected-items="handleSelectedItems"/>
                <div class="d-flex flex-row flex-wrap justify-content-between">
                    <div class="d-flex flex-column">
                        <p class="select-header">CT Scan</p>
                        <form-select :optionsData="ctScan"/>
                    </div>
                    <div class="d-flex flex-column">
                        <p class="select-header">MRI</p>
                        <form-select :optionsData="mriScan"/>
                    </div>
                </div>
               <div class="d-flex justify-content-end mt-3 mt-md-4 mb-5 ">
                <b-button @click="handleSubmit" style="background-color: #382F90;">Save and Send</b-button>

                <success-modal :show-modal="showModal" @close-modal="closeModal" />

               </div>
            </div>
        </div>
    </div>
</template>
<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Lato');

#backboard {
    background-color:#F5F5FB ;
    margin: 0;
    padding: 0;
    gap: 30px;
}

    .header1-purple {
        font-size: 32px;
        line-height: 44px;
        color: #382F90;
    }
    .avenir-normal-900 {
        font-family: 'Avenir';
        font-style: normal;
        font-weight: 900;
    }
    .sub-text-grey {
        font-family: 'Avenir';
        font-style: normal;
        font-weight: 500;
        font-size: 16px;
        line-height: 20px;
        letter-spacing: 0.3px;
        color: #9FA2B4;
    }
    #main {
        margin-left: 25vw;
        width: 70vw;
    }
    #form-checkbox {
        background-color: white;
        width: 70vw;
        font-family: 'Lato';
        font-style: normal;
        font-weight: 700;
        font-size: 14px;
    }
    .select-header {
        margin-bottom: 0;

color: #9FA2B4;
    }
    @media (max-width: 809px) {
        #main {
            margin-left:10vw;
            width: 80vw;
        }
}

</style>
<script>
import FormSelect from './FormSelect.vue'
import SideNav from './SideNav.vue';
import CheckBoxGroup from './CheckBoxGroup.vue';
import SuccessModal from './SuccessModal.vue'

export default {
    data() {
        return {
            investigations:[],
            ctScan: [{ value: 'Scan needed in the left cerebral hemisphere', text: 'Scan needed in the left cerebral hemisphere' }],
            mriScan: [{ value: 'Full body MRI', text: 'Full body MRI' }],
            selectedItemsArray:[],
            showModal: false,
            isDisabled: true
        }
        
    },
    computed: {
      hasSelectedItems() {
        return this.selectedItemsArray.length > 0;
      }
    },
    methods: {
        async handleSubmit() {

        // Make sure at least one checkbox is selected
        if (this.selectedItems.length === 0) {
            alert('Please select at least one checkbox');
            return;
        }
    // Make the POST request
    await fetch("http://testdrive.kompletecare.com/api/investigations", {
      method: "POST",
      headers: {
        "Content-Type": "application/json"
      },
      body: JSON.stringify({
        investigations: this.selectedItems,
        ctscan: "Scan Needed In The Left Cerebral Hemisphere",
        mri: "Full Body MRI",
        developer: "Developer"
      })
    });

    // Show the success modal
    this.showModal = true;
  },
  closeModal() {
    this.showModal = false;
  }, 

    },
    components: {
        'form-select':FormSelect,
        'SideNav': SideNav,
        'CheckBoxGroup' : CheckBoxGroup,
        'success-modal': SuccessModal

    },
    watch: {
    selectedItemsArray() {
      this.$nextTick(() => {
        // Re-enable the button after a checkbox is clicked
        const button = document.getElementById("submitButton");
        button.disabled = this.selectedItemsArray.length === 0;
      });
    },
  },
    created() {
      const url = 'http://testdrive.kompletecare.com/api';
      const endpoint = url + '/investigations';
      const token = '5111|Vw8oJD9IhXgsUsWiRVcppNaeA7ow96QOyUaecwIX';

      fetch(endpoint, {
        method: 'GET',
        headers: {
          'Authorization': `Bearer ${token}`
        }
      })
        .then(response => response.json())
        .then(data => {
          this.investigations = data.data;

        })
        .catch(error => {
          console.error(error);
        });
    }
  
 
}
</script>
<template>
    <div>
        <span style="font-size:30px;cursor:pointer" @click="openSideNav">&#9776;</span>
        <nav class="d-flex flex-column justify-content-evenly pt-5 mt-5" id="side-panel">
        <a @click="closeSideNav" href="javascript:void(0)" class="closebtn">&times;</a>
            <a class="sidebar-list active d-flex flex-row p-2 align-items-center"><img class="pl-3 mr-4" src="../static/../static/dashboard-icon.svg"/> Dashboard</a>
            <a class="sidebar-list d-flex flex-row p-2 align-items-center"><img class="pl-3 mr-4" src="../static/profile-icon.svg"/>Profile</a>
            <a class="sidebar-list d-flex flex-row p-2 align-items-center"><img class="pl-3 mr-4" src="../static/services-icon.svg" />Services</a>
            <a class="sidebar-list d-flex flex-row p-2 align-items-center"><img class="pl-3 mr-4" src="../static/medical-records-icons.svg"/>Medical Records</a>
            <a class="sidebar-list d-flex flex-row p-2 align-items-center"><img class="pl-3 mr-4" src="../static/care-wallet-icon.svg" />Care Wallet</a>
            <a class="sidebar-list d-flex flex-row p-2 align-items-center"><img class="pl-3 mr-4" src="../static/messages-icon.svg"/>Messages</a>
            <a class="sidebar-list d-flex flex-row p-2 align-items-center"><img class="pl-3 mr-4" src="../static/resources-icon.svg" />Resources</a>
            <hr class="w-inherit"/>
            <a class="sidebar-list d-flex flex-row p-2 align-items-center"><img class="pl-3 mr-4" src="../static/account-settings-icon.svg"/>Account Settings</a>
            <a class="sidebar-list d-flex flex-row p-2 align-items-center"><img class="pl-3 mr-4" src="../static/contact-support-icon.svg" />Contact Support</a>
            <a class="sidebar-list d-flex flex-row p-2 align-items-center"><img class="pl-3 mr-4" src="../static/logout-icon.svg" />Logout</a>
            <i class="bi bi-list" @click="openSideNav"></i>
        </nav>
    </div>
    
        
</template>

<style scoped>
.sidebar-list:hover{
        background-color: #2A36A4;
}
.active {
    background-color: #2A36A4;
    color: white;
}
nav {
    background-color: #FFFFFF;
    width: 25vw;
    height: 100%;
    position: fixed;
    z-index: 1;
    top: 0;
    left: 0;
    overflow-x: hidden;
    transition: 0.5s;
    padding-top: 60px;
}
nav a{
    font-family: "Product Sans";
    cursor: pointer;
    text-decoration: none;
    transition: 0.3s;
    color: #A0A0A0;
}
nav .closebtn {
  position: absolute;
  top: 0;
  right: 35px;
  font-size: 36px;
  margin-left: 50px;
}
.w-inherit {
    width: inherit;
}
span {
    position: fixed;
    top: 50px;
    left: 20px;
    padding: 2px;
    height: fit-content;
}
@media screen and (max-height: 450px) {
  nav {padding-top: 15px;}
  nav a {font-size: 18px;}
}

@media (min-width: 810px) {
    span {
        display: none;
    }
    nav .closebtn {
        display: none;
    }

}
@media (max-width: 809px) {
    nav{
        width: 0;
    }
}
</style>

<script>
export default {
    methods: {
        openSideNav() {
            
            document.getElementById("side-panel").style.width = "60vw";
        },
        closeSideNav() {
            document.getElementById("side-panel").style.width = "0";
           
        }
    }
}
</script>
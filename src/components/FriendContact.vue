


<template>
     <li>
          <h2>{{ name }} {{ isFavorite ? '(Favourite)' : '' }}</h2>
          <button @click="toggleFavorite">Favourite</button>
          <button @click="deatailsVisibility">{{ areDetailsVisible ? 'Hide ' : 'Show '}} Details</button>
          <ul v-if="areDetailsVisible">
            <li><strong>Phone:</strong>{{ phoneNumber }}</li>
            <li><strong>Email:</strong>{{ emailAddress }}</li>
          </ul>
          <button @click="deleteContact" >Delete Contact</button>
        </li>
</template>

<script>
export default{
    //Vue components require explicit props declaration so that Vue knows what external props passed to
    // the component should be treated as fallthrough attributes

    //We declare long prop names using camelCase because this avoids having to use quotes when using them as property keys,
    // and allows us to reference them directly in template expressions because they are valid JavaScript identifiers:

    //Technically, you can also use camelCase when passing props to a child component (except in DOM templates). 
    //However, the convention is using kebab-case in all cases to align with HTML attributes:
    // props: [
    //     'name',
    //     'phoneNumber',
    //     'emailAddress',
    //     'isFavorite'
    // ],
    //Props are there to send data into a component 
    props: {
        id: {
            type: String,
            required: true,
        },
        name: {
            type: String,
            required: true,
        },
        phoneNumber: {
            type: Number,
            required: true,
        },
        emailAddress:{
            type: String,
            required: true,
        },
        isFavorite: {
            type: Boolean,
            required: false,
            default: false,
            // validator: function(value){
            //     return value === '1' || value === '0';
            // }
        },
        
    },
    //Emits are there to send data out of the component
    emits: ['toggle-favorite'],
        // emits:{
        //     'toggle-favorite': function(id){
        //         if(id){
        //             return true;
        //         }else{
        //             console.warn('Id is missing')
        //             return false;
        //         }
        //     }
        // }
    data() {
        return {
            areDetailsVisible: false,
            friend: {
                id: 'Hirwa',
                name: 'Hirwa Jean Pippen',
                phone: 48123457,
                email: 'hirwajean@hotmail.com'
            },
            
        }
    },
    methods: {
        deatailsVisibility(){
            this.areDetailsVisible = !this.areDetailsVisible;
        },
        toggleFavorite(){
            //to setup communication from the friendContact Component.vue to the parent App.vue  
            this.$emit('toggle-favorite', this.id);//kebab-case is recommended for event listeners in templates.
        },
        deleteContact(){
            this.$emit('delete', this.id);
        }
    }
}
</script>



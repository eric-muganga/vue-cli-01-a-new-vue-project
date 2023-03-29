
<template>
     <li>
          <h2>{{ name }} {{ this.friendIsFavorite === '1' ? '(Favourite)' : '' }}</h2>
          <button @click="toggleFavorite">Favourite</button>
          <button @click="deatailsVisibility">{{ areDetailsVisible ? 'Hide ' : 'Show '}} Details</button>
          <ul v-if="areDetailsVisible">
            <li><strong>Phone:</strong>{{ phoneNumber }}</li>
            <li><strong>Email:</strong>{{ emailAddress }}</li>
          </ul>
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
    props: {
        name: {
            type: String,
            required: true,
        },
        phoneNumber: {
            type: String,
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
    data() {
        return {
            areDetailsVisible: false,
            friend: {
                id: 'Hirwa',
                name: 'Hirwa Jean Pippen',
                phone: 48123457,
                email: 'hirwajean@hotmail.com'
            },
            friendIsFavorite:this.isFavorite,
        }
    },
    methods: {
        deatailsVisibility(){
            this.areDetailsVisible = !this.areDetailsVisible;
        },
        toggleFavorite(){
            if(this.friendIsFavorite === '1'){
                this.friendIsFavorite = '0;'
            }else{
                this.friendIsFavorite = '1';
            }
        }
    }
}
</script>

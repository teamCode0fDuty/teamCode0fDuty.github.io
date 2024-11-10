<div class="text-white flex justify-center mt-10">
   <div class="flex justify-center flex-col text-center w-1/2">
     <h1 class="text-2xl font-bold mb-5">
      Our Menu
    </h1>
     <p class="text-base">
      "Brew and Buns: Where every sip of coffee meets the perfect bite of 
      a bun—an unforgettable taste experience awaits you!"
     </p>
   </div>
</div>

<!--Product List-->

<script lang="ts">
   // Declare cart modal element
   let cartModal: HTMLDivElement | null = null;
   
   // Define cart items and the list of products
   let cartItems: { id: number; name: string; price: number }[] = [];
   let totalPrice: number = 0;
   
   let products = [
     { id: 1, name: 'Cappuccino', price: 120, image: '/assets/capuccino.png' },
     { id: 2, name: 'Croissant', price: 75, image: '/assets/croissant.png' },
     { id: 3, name: 'Mini Donut', price: 5, image: '/assets/mini-donut.png' },
     { id: 4, name: 'Cold Brewed Coffee', price: 45, image: '/assets/cold.png' },
     { id: 5, name: 'Black Coffee', price: 25, image: '/assets/black.png' }
   ];
 
   // Function to add product to cart
   const addToCart = (product: { id: number; name: string; price: number }) => {
     // Add the product to the cart
     cartItems = [...cartItems, product];
     totalPrice = cartItems.reduce((total, item) => total + item.price, 0);
   };
 
   // Function to remove product from cart
   const removeFromCart = (productId: number) => {
     // Filter out the product with the matching ID
     cartItems = cartItems.filter(item => item.id !== productId);
     totalPrice = cartItems.reduce((total, item) => total + item.price, 0);
   };
 
   // Open the cart modal
   let isCartModalOpen = false;
   const openCartModal = () => {
     isCartModalOpen = true;
   };
 
   // Close the cart modal
   const closeCartModal = () => {
     isCartModalOpen = false;
   };
 </script>
 
 <div class="p-4">
   
   <div class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-5 gap-4">
     {#each products as product}
       <div class="bg-[rgba(151,151,151,0.25)] p-4 rounded-lg">
         <img src={product.image} alt={product.name} class="w-full h-48 object-cover mb-4" />
         <h3 class="text-xl font-semibold">{product.name}</h3>
         <p class="text-gray-600">Price: ${product.price}</p>
         <button
           class="mt-2 bg-blue-500 text-white py-2 px-4 rounded hover:bg-blue-600"
           on:click={() => addToCart(product)}
         >
           Add to Cart
         </button>
       </div>
     {/each}
   </div>
 
   <!-- Button to view cart -->
   <button
     class="mt-6 bg-green-500 text-white py-2 px-6 rounded hover:bg-green-600"
     on:click={openCartModal}
   >
     View Cart
   </button>
 
   <!-- Cart Modal -->
   <div
     class={`fixed inset-0 bg-gray-500 bg-opacity-50 flex justify-center items-center ${isCartModalOpen ? '' : 'hidden'}`}
   >
     <div class="bg-white p-6 rounded-lg shadow-lg w-96">
       <h2 class="text-2xl font-semibold mb-4">Your Cart</h2>
       {#if cartItems.length > 0}
         <ul class="space-y-4">
           {#each cartItems as item}
             <li class="flex justify-between items-center">
               <span>{item.name} - ${item.price}</span>
               <button
                 class="bg-red-500 text-white py-1 px-2 rounded hover:bg-red-600"
                 on:click={() => removeFromCart(item.id)}
               >
                 Remove
               </button>
             </li>
           {/each}
         </ul>
         <p class="mt-4 text-xl font-semibold">Total: ${totalPrice}</p>
       {:else}
         <p class="text-gray-600">Your cart is empty</p>
       {/if}
       <button
         class="mt-4 bg-gray-500 text-white py-2 px-6 rounded hover:bg-gray-600"
         on:click={closeCartModal}
       >
         Close
       </button>
     </div>
   </div>
 </div>
 
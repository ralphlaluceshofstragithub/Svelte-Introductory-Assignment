<grocery-item-list>
  {#each grocery_item_list as grocery_item}
    <grocery-item>
      <input type="text" name="name"        bind:value={grocery_item.name}/> 
      $  <input type="number" name="price"  bind:value={grocery_item.price}/>
    </grocery-item>
  {/each}
</grocery-item-list>

<button on:click = {add_item} >
  Add grocery item  
</button>

<grocery-total>
  {grocery_item_list.length} items ${total} Total 
</grocery-total>

<style>
	grocery-item-list{
    background-color: khaki;
    display: grid;
  }
</style>

<script>

	class GroceryItem{
    constructor(values){
      this.name = values.name
      this.price = values.price
    }
  }

  let grocery_item_list = [
    new GroceryItem({name: "Chicken" , price:7.50}),
    new GroceryItem({name: "Soup"    , price:1.99}),
    new GroceryItem({name: "Pasta"   , price:2.99}),
    new GroceryItem({name: "Potatoes", price:2.49})
  ]
   

  let total
  
  $: total = grocery_item_list.reduce((sum, item) => sum + item.price, 0)

  console.log(grocery_item_list)

  const add_item = () => {
    const new_item = new GroceryItem({name: "New Item", price:0})
    grocery_item_list = grocery_item_list.concat([new_item])
  }
</script>


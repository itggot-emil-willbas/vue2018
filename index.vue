  

    <div id="app">
        <h1>Vi har {{thing}}</h1>
        <ul>
            <li v-for="product in products">
                <input type="number" v-model.number="product.quantity">
                {{product.name}}
                <span v-if="product.quantity === 0">- OUT OF STOCK</span>
                <button @click="product.quantity += 1">add</button>
            </li>
        </ul>
        <h2>Total inventory: {{ totalProducts }}</h2>
    </div>
    <script src="https://unpkg.com/vue"></script>
    <script>
    const app = new Vue({
        el:"#app",
        data: {
            thing:'Boots',
            products:[]
        },
        computed: {
            totalProducts () {
                return this.products.reduce((sum,product) => { //sum alla värden, product det sista (current)
                    return sum + product.quantity
                }, 0)
            }
        },
        created () {
            fetch('https://api.myjson.com/bins/74l63')
                .then(response => response.json())
                .then(json => {
                    this.products = json.products
                })
        }
    })
    </script>

<script>
    let products = [
        { id: 1, name: "Product 1", price: 10.0 },
        { id: 2, name: "Product 2", price: 20.0 },
    ];

    let newProduct = { name: "", price: 0 };
    let editProduct = null;

    // Add a new product
    function addProduct() {
        if (newProduct.name && newProduct.price > 0) {
            products = [...products, { ...newProduct, id: products.length + 1 }];
            newProduct = { name: "", price: 0 };
        }
    }

    // Start editing a product
    function startEdit(product) {
        editProduct = { ...product };
    }

    // Update the edited product
    function updateProduct() {
        if (editProduct.name && editProduct.price > 0) {
            products = products.map((p) =>
                p.id === editProduct.id ? { ...editProduct } : p
            );
            editProduct = null;
        }
    }

    // Delete a product
    function deleteProduct(id) {
        products = products.filter((product) => product.id !== id);
    }
</script>

<style>
    table {
        width: 100%;
        margin-top: 20px;
        border-collapse: collapse;
    }

    table,
    th,
    td {
        border: 1px solid black;
    }

    th,
    td {
        padding: 10px;
        text-align: left;
    }

    input {
        margin: 5px;
    }
</style>

<h1>Product Management (Client-side)</h1>

<!-- Add new product -->
<div>
    <input bind:value={newProduct.name} placeholder="Product name" />
    <input type="number" bind:value={newProduct.price} placeholder="Product price" />
    <button on:click={addProduct}>Add Product</button>
</div>

<!-- Edit product -->
{#if editProduct}
    <div>
        <h3>Edit Product</h3>
        <input bind:value={editProduct.name} placeholder="Product name" />
        <input type="number" bind:value={editProduct.price} placeholder="Product price" />
        <button on:click={updateProduct}>Update Product</button>
        <button on:click={() => (editProduct = null)}>Cancel</button>
    </div>
{/if}

<!-- Display products -->
<table>
    <thead>
        <tr>
            <th>Id</th>
            <th>Name</th>
            <th>Price</th>
            <th>Actions</th>
        </tr>
    </thead>
    <tbody>
        {#each products as product}
            <tr>
                <td>{product.id}</td>
                <td>{product.name}</td>
                <td>{product.price}</td>
                <td>
                    <button on:click={() => startEdit(product)}>Edit</button>
                    <button on:click={() => deleteProduct(product.id)}>Delete</button>
                </td>
            </tr>
        {/each}
    </tbody>
</table>

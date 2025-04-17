import React, { useState } from "react";

export default function Timerbro() {
  const [showForm, setShowForm] = useState(false);
  const [selectedProduct, setSelectedProduct] = useState(null);

  const handleOrderClick = (i) => {
    setSelectedProduct(i);
    setShowForm(true);
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    const formData = new FormData(e.target);
    const userDetails = Object.fromEntries(formData.entries());
    console.log("Order Placed For:", selectedProduct + 1);
    console.log("User Details:", userDetails);
    alert("Order placed successfully!");
    setShowForm(false);
  };

  return (
    <div className="bg-black text-white min-h-screen">
      {/* Header */}
      <header className="p-4 flex justify-between items-center border-b border-gray-800">
        <h1 className="text-2xl font-bold text-yellow-400">TIMERBRO</h1>
        <nav>
          <ul className="flex gap-4">
            <li>Home</li>
            <li>Products</li>
            <li>Contact</li>
          </ul>
        </nav>
      </header>

      {/* Hero Section */}
      <section className="p-8 text-center">
        <h2 className="text-4xl font-semibold mb-2">Time. Reinvented.</h2>
        <p className="text-lg text-gray-400">
          Premium Smartwatches | Cash on Delivery
        </p>
      </section>

      {/* Product Grid */}
      <section className="grid grid-cols-2 md:grid-cols-4 gap-4 px-4">
        {[...Array(20)].map((_, i) => (
          <div key={i} className="bg-white text-black p-3 rounded-xl shadow-md">
            <img
              src={`/products/watch${i + 1}.jpg`}
              alt={`Watch ${i + 1}`}
              className="w-full h-40 object-cover rounded mb-2"
            />
            <h3 className="font-semibold">Product {i + 1}</h3>
            <p className="text-sm">Smartwatch Model</p>
            <p className="text-md font-bold text-green-600 mt-1">
              ₹999 <span className="text-gray-500 line-through text-sm ml-2">₹3999</span>
            </p>
            <p className="text-xs text-red-500 font-semibold">75% OFF</p>
            <button
              className="mt-2 px-4 py-1 bg-black text-white rounded"
              onClick={() => handleOrderClick(i)}
            >
              Order Now
            </button>
          </div>
        ))}
      </section>

      {/* Checkout Form */}
      {showForm && (
        <div className="fixed top-0 left-0 w-full h-full bg-black bg-opacity-80 flex items-center justify-center z-50">
          <form
            onSubmit={handleSubmit}
            className="bg-white text-black p-6 rounded-lg w-11/12 max-w-md"
          >
            <h3 className="text-xl font-bold mb-4 text-center">Checkout Form</h3>
            <input name="name" required placeholder="Full Name" className="mb-2 p-2 w-full border rounded" />
            <input name="mobile" required placeholder="Mobile Number" className="mb-2 p-2 w-full border rounded" />
            <input name="house" required placeholder="House No." className="mb-2 p-2 w-full border rounded" />
            <input name="landmark" required placeholder="Landmark" className="mb-2 p-2 w-full border rounded" />
            <input name="city" required placeholder="City" className="mb-2 p-2 w-full border rounded" />
            <input name="pincode" required placeholder="Pin Code" className="mb-2 p-2 w-full border rounded" />
            <input name="state" required placeholder="State" className="mb-2 p-2 w-full border rounded" />
            <button type="submit" className="bg-yellow-500 text-white w-full p-2 rounded mt-2">Place Order</button>
            <button
              type="button"
              onClick={() => setShowForm(false)}
              className="w-full mt-2 text-sm text-gray-600 underline"
            >
              Cancel
            </button>
          </form>
        </div>
      )}

      {/* Footer */}
      <footer className="mt-10 text-center text-sm text-gray-500 p-4 border-t border-gray-800">
        &copy; 2025 Timerbro. All rights reserved.
      </footer>
    </div>
  );
}

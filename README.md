# Shipments.jsx
import React, { useState } from 'react';
import '../styles/Shipments.css';

const Shipments = () => {
  const [searchTerm, setSearchTerm] = useState('');
  const [statusFilter, setStatusFilter] = useState('');
  const [subCategoryFilter, setSubCategoryFilter] = useState('');
  const [subSubCategoryFilter, setSubSubCategoryFilter] = useState('');
  const [wishlist, setWishlist] = useState([]);
  const [cart, setCart] = useState([]);
  const [viewedProducts, setViewedProducts] = useState([]);

  const [shipments, setShipments] = useState([
    
    {
    id: 1,
    name: 'Denim Jeans',
    mainCategory: 'Fashion',
    subCategory: "Men's Wear",
    subSubCategory: 'Jeans',
    origin: 'Mumbai',
    destination: 'Delhi',
    date: '2025-08-05',
    status: 'Pending',
    price: '999',
    imageUrl: '' // ✅ Jeans
  },
  {
    id: 2,
    name: 'Floral Gown',
    mainCategory: 'Fashion',
    subCategory: "Women's Wear",
    subSubCategory: 'Gowns',
    origin: 'Pune',
    destination: 'Bangalore',
    date: '2025-08-04',
    status: 'In Transit',
    price: '1499',
    imageUrl: '' // ✅ Gown
  },
  {
    id: 3,
    name: 'Western Top',
    mainCategory: 'Fashion',
    subCategory: "Women's Wear",
    subSubCategory: 'Western Wear',
    origin: 'Kolkata',
    destination: 'Lucknow',
    date: '2025-08-02',
    status: 'Delivered',
    price: '799',
    imageUrl: '' // ✅ Top
  },
  {
    id: 4,
    name: 'Blazer Suit',
    mainCategory: 'Fashion',
    subCategory: "Men's Wear",
    subSubCategory: 'Suits',
    origin: 'Chennai',
    destination: 'Hyderabad',
    date: '2025-08-01',
    status: 'Pending',
    price: '1999',
    imageUrl: '' // ✅ Suit
  }
]);

  const handleDelete = (id) => {
    const updatedShipments = shipments.filter(shipment => shipment.id !== id);
    setShipments(updatedShipments);
  };

  const handleBuyNow = (shipment) => {
    setCart(prev => [...prev, shipment]);
    alert(`Proceeding to Buy: ${shipment.name} - ₹${shipment.price}`);
  };

  const handleAddToCart = (shipment) => {
    if (!cart.some(item => item.id === shipment.id)) {
      setCart(prev => [...prev, shipment]);
      alert(`Added to Cart: ${shipment.name}`);
    } else {
      alert(`${shipment.name} is already in your cart.`);
    }
  };

  const handleAddToWishlist = (shipment) => {
    if (!wishlist.some(item => item.id === shipment.id)) {
      setWishlist(prev => [...prev, shipment]);
      alert(`Added to Wishlist: ${shipment.name}`);
    } else {
      alert(`${shipment.name} is already in your wishlist.`);
    }
  };

  const handleViewDetails = (shipment) => {
    if (!viewedProducts.some(item => item.id === shipment.id)) {
      setViewedProducts(prev => [...prev, shipment]);
    }
    alert(`Viewing details for: ${shipment.name}`);
  };

  const filteredShipments = shipments.filter((shipment) => {
    return (
      shipment.name.toLowerCase().includes(searchTerm.toLowerCase()) &&
      (!statusFilter || shipment.status === statusFilter) &&
      (!subCategoryFilter || shipment.subCategory === subCategoryFilter) &&
      (!subSubCategoryFilter || shipment.subSubCategory === subSubCategoryFilter)
    );
  });

  return (
    <div className="shipments-container">
      <h2 className="shipments-title">All Shipments</h2>
      <div className="filter-bar">
        <input
          type="text"
          placeholder="Search products..."
          value={searchTerm}
          onChange={(e) => setSearchTerm(e.target.value)}
        />
        <select value={statusFilter} onChange={(e) => setStatusFilter(e.target.value)}>
          <option value="">All Statuses</option>
           <option value="picked up">Picked up</option>
          <option value="Pending">Pending</option>
          <option value="In Transit">In Transit</option>
          <option value="Delivered">Delivered</option>
          <option value="Cancled">Cancled</option>
        </select>
        <select value={subCategoryFilter} onChange={(e) => setSubCategoryFilter(e.target.value)}>
          <option value="">All Gender Categories</option>
          <option value="Men's Wear">Men's Wear</option>
          <option value="Women's Wear">Women's Wear</option>
        </select>
        <select value={subSubCategoryFilter} onChange={(e) => setSubSubCategoryFilter(e.target.value)}>
          <option value="">All Subcategories</option>
          <option value="Tops">Tops</option>
          <option value="Jeans">Jeans</option>
          <option value="Jackets">Jackets</option>
          <option value="Suits">Suits</option>
          <option value="Gowns">Gowns</option>
          <option value="Ethnic Wear">Ethnic Wear</option>
          <option value="Western Wear">Western Wear</option>
        </select>
      </div>

      <div className="shipments-grid">
        {filteredShipments.map((shipment) => (
          <div key={shipment.id} className="shipment-card">
            <img src={shipment.imageUrl} alt={shipment.name} className="shipment-image" />
            <div className="shipment-details">
              <h3 className="shipment-name">{shipment.name}</h3>
              <p className="shipment-category">{shipment.mainCategory} - {shipment.subCategory} - {shipment.subSubCategory}</p>
              <p><strong>From:</strong> {shipment.origin}</p>
              <p><strong>To:</strong> {shipment.destination}</p>
              <p><strong>Date:</strong> {shipment.date}</p>
              <p><strong>Status:</strong> {shipment.status}</p>
              <p className="shipment-price"><strong>Price:</strong> ₹{shipment.price}</p>
              <div className="shipment-actions">
                <button className="details-button" onClick={() => handleViewDetails(shipment)}>View</button>
                <button className="buy-button" onClick={() => handleBuyNow(shipment)}>Buy Now</button>
                <button className="cart-button" onClick={() => handleAddToCart(shipment)}>Add to Cart</button>
                <button className="wishlist-button" onClick={() => handleAddToWishlist(shipment)}>Wishlist</button>
                <button className="delete-button" onClick={() => handleDelete(shipment.id)}>Remove</button>
              </div>
            </div>
          </div>
        ))}
      </div>
    </div>
  );
};

export default Shipments;import React, { useState } from 'react';
import '../styles/Shipments.css';

const Shipments = () => {
  const [searchTerm, setSearchTerm] = useState('');
  const [statusFilter, setStatusFilter] = useState('');
  const [subCategoryFilter, setSubCategoryFilter] = useState('');
  const [subSubCategoryFilter, setSubSubCategoryFilter] = useState('');
  const [wishlist, setWishlist] = useState([]);
  const [cart, setCart] = useState([]);
  const [viewedProducts, setViewedProducts] = useState([]);

  const [shipments, setShipments] = useState([
    
    {
    id: 1,
    name: 'Denim Jeans',
    mainCategory: 'Fashion',
    subCategory: "Men's Wear",
    subSubCategory: 'Jeans',
    origin: 'Mumbai',
    destination: 'Delhi',
    date: '2025-08-05',
    status: 'Pending',
    price: '999',
    imageUrl: '' // ✅ Jeans
  },
  {
    id: 2,
    name: 'Floral Gown',
    mainCategory: 'Fashion',
    subCategory: "Women's Wear",
    subSubCategory: 'Gowns',
    origin: 'Pune',
    destination: 'Bangalore',
    date: '2025-08-04',
    status: 'In Transit',
    price: '1499',
    imageUrl: '' // ✅ Gown
  },
  {
    id: 3,
    name: 'Western Top',
    mainCategory: 'Fashion',
    subCategory: "Women's Wear",
    subSubCategory: 'Western Wear',
    origin: 'Kolkata',
    destination: 'Lucknow',
    date: '2025-08-02',
    status: 'Delivered',
    price: '799',
    imageUrl: '' // ✅ Top
  },
  {
    id: 4,
    name: 'Blazer Suit',
    mainCategory: 'Fashion',
    subCategory: "Men's Wear",
    subSubCategory: 'Suits',
    origin: 'Chennai',
    destination: 'Hyderabad',
    date: '2025-08-01',
    status: 'Pending',
    price: '1999',
    imageUrl: '' // ✅ Suit
  }
]);

  const handleDelete = (id) => {
    const updatedShipments = shipments.filter(shipment => shipment.id !== id);
    setShipments(updatedShipments);
  };

  const handleBuyNow = (shipment) => {
    setCart(prev => [...prev, shipment]);
    alert(`Proceeding to Buy: ${shipment.name} - ₹${shipment.price}`);
  };

  const handleAddToCart = (shipment) => {
    if (!cart.some(item => item.id === shipment.id)) {
      setCart(prev => [...prev, shipment]);
      alert(`Added to Cart: ${shipment.name}`);
    } else {
      alert(`${shipment.name} is already in your cart.`);
    }
  };

  const handleAddToWishlist = (shipment) => {
    if (!wishlist.some(item => item.id === shipment.id)) {
      setWishlist(prev => [...prev, shipment]);
      alert(`Added to Wishlist: ${shipment.name}`);
    } else {
      alert(`${shipment.name} is already in your wishlist.`);
    }
  };

  const handleViewDetails = (shipment) => {
    if (!viewedProducts.some(item => item.id === shipment.id)) {
      setViewedProducts(prev => [...prev, shipment]);
    }
    alert(`Viewing details for: ${shipment.name}`);
  };

  const filteredShipments = shipments.filter((shipment) => {
    return (
      shipment.name.toLowerCase().includes(searchTerm.toLowerCase()) &&
      (!statusFilter || shipment.status === statusFilter) &&
      (!subCategoryFilter || shipment.subCategory === subCategoryFilter) &&
      (!subSubCategoryFilter || shipment.subSubCategory === subSubCategoryFilter)
    );
  });

  return (
    <div className="shipments-container">
      <h2 className="shipments-title">All Shipments</h2>
      <div className="filter-bar">
        <input
          type="text"
          placeholder="Search products..."
          value={searchTerm}
          onChange={(e) => setSearchTerm(e.target.value)}
        />
        <select value={statusFilter} onChange={(e) => setStatusFilter(e.target.value)}>
          <option value="">All Statuses</option>
           <option value="picked up">Picked up</option>
          <option value="Pending">Pending</option>
          <option value="In Transit">In Transit</option>
          <option value="Delivered">Delivered</option>
          <option value="Cancled">Cancled</option>
        </select>
        <select value={subCategoryFilter} onChange={(e) => setSubCategoryFilter(e.target.value)}>
          <option value="">All Gender Categories</option>
          <option value="Men's Wear">Men's Wear</option>
          <option value="Women's Wear">Women's Wear</option>
        </select>
        <select value={subSubCategoryFilter} onChange={(e) => setSubSubCategoryFilter(e.target.value)}>
          <option value="">All Subcategories</option>
          <option value="Tops">Tops</option>
          <option value="Jeans">Jeans</option>
          <option value="Jackets">Jackets</option>
          <option value="Suits">Suits</option>
          <option value="Gowns">Gowns</option>
          <option value="Ethnic Wear">Ethnic Wear</option>
          <option value="Western Wear">Western Wear</option>
        </select>
      </div>

      <div className="shipments-grid">
        {filteredShipments.map((shipment) => (
          <div key={shipment.id} className="shipment-card">
            <img src={shipment.imageUrl} alt={shipment.name} className="shipment-image" />
            <div className="shipment-details">
              <h3 className="shipment-name">{shipment.name}</h3>
              <p className="shipment-category">{shipment.mainCategory} - {shipment.subCategory} - {shipment.subSubCategory}</p>
              <p><strong>From:</strong> {shipment.origin}</p>
              <p><strong>To:</strong> {shipment.destination}</p>
              <p><strong>Date:</strong> {shipment.date}</p>
              <p><strong>Status:</strong> {shipment.status}</p>
              <p className="shipment-price"><strong>Price:</strong> ₹{shipment.price}</p>
              <div className="shipment-actions">
                <button className="details-button" onClick={() => handleViewDetails(shipment)}>View</button>
                <button className="buy-button" onClick={() => handleBuyNow(shipment)}>Buy Now</button>
                <button className="cart-button" onClick={() => handleAddToCart(shipment)}>Add to Cart</button>
                <button className="wishlist-button" onClick={() => handleAddToWishlist(shipment)}>Wishlist</button>
                <button className="delete-button" onClick={() => handleDelete(shipment.id)}>Remove</button>
              </div>
            </div>
          </div>
        ))}
      </div>
    </div>
  );
};

export default Shipments;
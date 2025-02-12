i mport Image from 'next/image';
import Link from 'next/link';

export default function Home() {
  return (
    <div className="min-h-screen bg-gray-100">
      {/* الهيدر */}
      <header className="bg-white shadow-md py-4 px-6 flex justify-between items-center">
        <h1 className="text-2xl font-bold">
          <span className="text-blue-600">S</span>tride
        </h1>
        <Link href="/cart" className="bg-blue-600 text-white px-4 py-2 rounded">
          سلة المشتريات 🛒
        </Link>
      </header>

      {/* المحتوى الرئيسي */}
      <main className="container mx-auto py-10 px-6">
        <h2 className="text-3xl font-semibold mb-6">أحدث المنتجات</h2>
        
        {/* عرض المنتجات */}
        <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
          <div className="bg-white p-4 rounded-lg shadow-md">
            <Image src="/product1.jpg" width={300} height={200} alt="منتج 1" className="rounded-md"/>
            <h3 className="text-lg font-semibold mt-2">حذاء رياضي</h3>
            <p className="text-gray-600">أفضل جودة وأداء.</p>
            <button className="mt-3 bg-blue-600 text-white px-4 py-2 rounded">
              إضافة للسلة
            </button>
          </div>
        </div>
      </main>
    </div>
  );
}
import { useState, useEffect } from 'react';
import Image from 'next/image';

export default function Products() {
  const [products, setProducts] = useState([]);

  useEffect(() => {
    fetch('/products.json')
      .then((res) => res.json())
      .then((data) => setProducts(data));
  }, []);

  return (
    <div className="container mx-auto py-10 px-6">
      <h2 className="text-3xl font-semibold mb-6">المنتجات المتاحة</h2>
      <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
        {products.map((product) => (
          <div key={product.id} className="bg-white p-4 rounded-lg shadow-md">
            <Image src={product.image} width={300} height={200} alt={product.name} className="rounded-md"/>
            <h3 className="text-lg font-semibold mt-2">{product.name}</h3>
            <p className="text-gray-600">{product.description}</p>
            <button className="mt-3 bg-blue-600 text-white px-4 py-2 rounded">
              إضافة للسلة
            </button>
          </div>
        ))}
      </div>
    </div>
  );
}
import { useState } from 'react';

export default function Cart() {
  const [cart, setCart] = useState([]);

  return (
    <div className="container mx-auto py-10 px-6">
      <h2 className="text-3xl font-semibold mb-6">سلة المشتريات 🛒</h2>
      {cart.length === 0 ? (
        <p className="text-gray-600">السلة فارغة</p>
      ) : (
        <ul>
          {cart.map((item, index) => (
            <li key={index} className="bg-white p-4 rounded-lg shadow-md mb-4">
              {item.name} - {item.price} جنيه
            </li>
          ))}
        </ul>
      )}
      <button className="mt-3 bg-green-600 text-white px-4 py-2 rounded">
        إتمام الطلب
      </button>
    </div>
  );
}
@tailwind base;
@tailwind components;
@tailwind utilities;

body {
  font-family: Arial, sans-serif;
  background-color: #f7f7f7;
}
[
  {
    "id": 1,
    "name": "حذاء رياضي",
    "description": "أفضل جودة وأداء.",
    "price": 500,
    "image": "/product1.jpg"
  },
  {
    "id": 2,
    "name": "تيشيرت رياضي",
    "description": "مصنوع من قماش مريح.",
    "price": 200,
    "image": "/product2.jpg"
  }
]
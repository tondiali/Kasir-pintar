import React, { useState } from "react"; import { Card, CardContent } from "@/components/ui/card"; import { Button } from "@/components/ui/button"; import { Input } from "@/components/ui/input";

export default function KasirPintar() { const [items, setItems] = useState([ { id: 1, name: "Pupuk Urea", price: 50000, stock: 10 }, { id: 2, name: "Benih Padi", price: 120000, stock: 5 }, { id: 3, name: "Pestisida", price: 75000, stock: 8 }, ]); const [cart, setCart] = useState([]);

const addToCart = (item) => { if (item.stock > 0) { setCart([...cart, item]); setItems( items.map((i) => (i.id === item.id ? { ...i, stock: i.stock - 1 } : i)) ); } };

const removeFromCart = (index) => { const newCart = [...cart]; const removedItem = newCart.splice(index, 1)[0]; setCart(newCart); setItems( items.map((i) => i.id === removedItem.id ? { ...i, stock: i.stock + 1 } : i ) ); };

const getTotal = () => { return cart.reduce((total, item) => total + item.price, 0); };

return ( <div className="p-4 max-w-md mx-auto"> <h1 className="text-xl font-bold mb-4">Kasir Pintar</h1> <div> {items.map((item) => ( <Card key={item.id} className="mb-2"> <CardContent className="flex justify-between items-center p-2"> <div> <p>{item.name}</p> <p className="text-sm text-gray-500">Rp{item.price} - Stok: {item.stock}</p> </div> <Button onClick={() => addToCart(item)} disabled={item.stock === 0}> Tambah </Button> </CardContent> </Card> ))} </div> <h2 className="text-lg font-semibold mt-4">Keranjang</h2> <div> {cart.map((item, index) => ( <Card key={index} className="mb-2"> <CardContent className="flex justify-between items-center p-2"> <p>{item.name}</p> <Button onClick={() => removeFromCart(index)}>Hapus</Button> </CardContent> </Card> ))} </div> <div className="mt-4 font-bold">Total: Rp{getTotal()}</div> <Button className="mt-2 w-full">Bayar</Button> </div> ); }

# Kasir-pintar

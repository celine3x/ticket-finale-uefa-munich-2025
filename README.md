# ticket-finale-uefa-munich-2025
import React, { useState } from "react";
import { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Calendar } from "@/components/ui/calendar";
import { CheckCircle, AlertTriangle, ShieldCheck, Lock, Flame } from "lucide-react";

export default function TicketFinalePage() {
  const [name, setName] = useState("");
  const [email, setEmail] = useState("");
  const [quantity, setQuantity] = useState(1);
  const [success, setSuccess] = useState(false);
  const [stock, setStock] = useState(250); // Nombre de billets disponibles

  const handlePurchase = (e) => {
    e.preventDefault();
    if (quantity > 0 && quantity <= stock) {
      setStock(stock - quantity);
      setSuccess(true);
    }
  };

  const isLowStock = stock <= 20;
  const isHotDemand = stock <= 100 && !success;

  return (
    <div className="min-h-screen bg-gradient-to-br from-blue-900 to-indigo-800 text-white p-6">
      <header className="text-center py-8">
        <h1 className="text-4xl font-bold">Finale Ligue des Champions 2025</h1>
        <p className="text-xl mt-2">Allianz Arena, Munich - 31 Mai 2025</p>
      </header>

      {isHotDemand && (
        <div className="max-w-2xl mx-auto mb-6 bg-red-600 text-white p-4 rounded-lg shadow-md flex items-center gap-3 animate-pulse">
          <Flame className="w-6 h-6" />
          <p className="text-sm font-medium">Forte demande ! Les billets partent très vite. Ne manquez pas votre chance !</p>
        </div>
      )}

      <main className="max-w-4xl mx-auto grid gap-8">
        {!success && (
          <Card className={`bg-white text-black shadow-lg rounded-2xl p-6 ${isLowStock ? 'border-2 border-red-500' : ''}`}>
            <CardContent>
              <h2 className="text-2xl font-semibold mb-4">Réservez vos billets</h2>
              <form className="grid gap-4" onSubmit={handlePurchase}>
                <Input
                  type="text"
                  placeholder="Nom complet"
                  value={name}
                  onChange={(e) => setName(e.target.value)}
                  required
                />
                <Input
                  type="email"
                  placeholder="Adresse email"
                  value={email}
                  onChange={(e) => setEmail(e.target.value)}
                  required
                />
                <Input
                  type="number"
                  placeholder="Nombre de billets"
                  value={quantity}
                  onChange={(e) => setQuantity(parseInt(e.target.value))}
                  required
                  min={1}
                  max={10}
                />
                <Calendar mode="single" selected={new Date("2025-05-31"))} disabled />
                <div className="bg-gray-100 text-black p-3 rounded-md">
                  <h3 className="text-md font-medium mb-2">Mode de paiement</h3>
                  <p className="text-sm">Paiement par virement bancaire. Les instructions vous seront envoyées par email après validation.</p>
                </div>
                <Button
                  className={`mt-4 ${isLowStock ? 'bg-red-600 hover:bg-red-700' : 'bg-blue-600 hover:bg-blue-700'}`}
                  type="submit"
                >
                  Acheter maintenant
                </Button>
              </form>
              <p className="mt-4 text-sm text-gray-600">Billets disponibles : {stock}</p>
              {isLowStock && (
                <div className="mt-2 text-red-600 flex items-center gap-2">
                  <AlertTriangle className="w-5 h-5" />
                  <span>Dépêchez-vous ! Moins de 20 billets restants.</span>
                </div>
              )}
            </CardContent>
          </Card>
        )}

        {success && (
          <div className="text-center">
            <CheckCircle className="mx-auto text-green-400 w-10 h-10 mb-2" />
            <p className="text-lg font-semibold">Achat confirmé pour {quantity} billet(s) !</p>
            <p className="text-sm">Un email de confirmation a été envoyé à {email}.</p>
          </div>
        )}

        {/* Section Sécurité & Confiance */}
        <Card className="bg-white text-black shadow-md rounded-2xl p-6">
          <CardContent>
            <h2 className="text-2xl font-semibold mb-4">Votre sécurité, notre priorité</h2>
            <div className="space-y-4 text-gray-700">
              <div className="flex items-start gap-3">
                <ShieldCheck className="text-green-600 mt-1" />
                <p className="text-sm">Toutes les transactions sont traitées manuellement pour garantir une vérification rigoureuse des paiements et des commandes.</p>
              </div>
              <div className="flex items-start gap-3">
                <Lock className="text-blue-600 mt-1" />
                <p className="text-sm">Vos données personnelles sont protégées et ne seront jamais partagées avec des tiers.</p>
              </div>
            </div>
          </CardContent>
        </Card>

        {/* Section FAQ et Contact */}
        <Card className="bg-white text-black shadow-md rounded-2xl p-6">
          <CardContent>
            <h2 className="text-2xl font-semibold mb-4">FAQ & Contact</h2>
            <div className="space-y-4">
              <div>
                <h3 className="text-lg font-medium">Comment vais-je recevoir mes billets ?</h3>
                <p className="text-sm text-gray-700">Une fois le virement bancaire confirmé, vos billets électroniques seront envoyés à votre adresse email.</p>
              </div>
              <div>
                <h3 className="text-lg font-medium">Puis-je obtenir un remboursement ?</h3>
                <p className="text-sm text-gray-700">Conformément à notre politique, aucun remboursement ne sera accordé sauf en cas d'annulation officielle de l'événement.</p>
              </div>
              <div>
                <h3 className="text-lg font-medium">Puis-je acheter plus de 10 billets ?</h3>
                <p className="text-sm text-gray-700">Pour des réservations de groupe, merci de nous contacter directement via le formulaire ci-dessous.</p>
              </div>
              <div className="mt-6">
                <h3 className="text-lg font-medium mb-2">Nous contacter</h3>
                <form className="grid gap-3">
                  <Input type="text" placeholder="Votre nom" required />
                  <Input type="email" placeholder="Votre email" required />
                  <textarea placeholder="Votre message" rows={4} className="p-2 border rounded-md" required />
                  <Button className="bg-blue-700 hover:bg-blue-800 mt-2" type="submit">Envoyer</Button>
                </form>
              </div>
            </div>
          </CardContent>
        </Card>
      </main>

      <footer className="text-center mt-12 text-sm text-gray-300">
        &copy; 2025 UEFA | Site non officiel pour la vente de billets
      </footer>
    </div>
  );
}

import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Tabs, TabsList, TabsTrigger, TabsContent } from "@/components/ui/tabs";

export default function LoboSolitarioScan() {
  const [isAdmin, setIsAdmin] = useState(false);
  const [obras, setObras] = useState([]);

  const handleUpload = (e) => {
    const file = e.target.files[0];
    if (file) {
      setObras([...obras, { nome: file.name }]);
    }
  };

  return (
    <div className="min-h-screen bg-black text-white p-6">
      <h1 className="text-3xl font-bold mb-6">🐺 Lobo Solitário Scan</h1>

      <Tabs defaultValue="inicial">
        <TabsList className="mb-4">
          <TabsTrigger value="inicial">Inicial</TabsTrigger>
          <TabsTrigger value="obras">Obras</TabsTrigger>
          <TabsTrigger value="comunidade">Comunidade</TabsTrigger>
        </TabsList>

        <TabsContent value="inicial">
          <Card className="bg-zinc-900">
            <CardContent className="p-6">
              <h2 className="text-xl font-semibold">Bem-vindo à Lobo Solitário Scan</h2>
              <p className="mt-2 text-gray-400">
                Leia Mangás, Manhwas e Manhuas online gratuitamente.
              </p>
            </CardContent>
          </Card>
        </TabsContent>

        <TabsContent value="obras">
          <div className="grid grid-cols-1 md:grid-cols-3 gap-4">
            {obras.map((obra, index) => (
              <Card key={index} className="bg-zinc-900">
                <CardContent className="p-4">
                  <h3 className="font-bold">{obra.nome}</h3>
                </CardContent>
              </Card>
            ))}
          </div>

          {isAdmin && (
            <div className="mt-6">
              <Input type="file" onChange={handleUpload} />
            </div>
          )}
        </TabsContent>

        <TabsContent value="comunidade">
          <Card className="bg-zinc-900">
            <CardContent className="p-6">
              <h2 className="text-xl font-semibold">Cadastro</h2>
              <div className="space-y-4 mt-4">
                <Input placeholder="Nome" />
                <Input placeholder="Email" type="email" />
                <Input placeholder="Senha" type="password" />
                <Button>Criar Conta</Button>
              </div>
            </CardContent>
          </Card>
        </TabsContent>
      </Tabs>

      <div className="mt-10">
        <Button onClick={() => setIsAdmin(!isAdmin)} variant="secondary">
          {isAdmin ? "Sair do modo Admin" : "Entrar como Admin"}
        </Button>
      </div>
    </div>
  );
}

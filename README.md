import React, { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { motion } from "framer-motion";

const agents = [
  { id: 1, name: "Escondedor", color: "bg-blue-400" },
  { id: 2, name: "Procurador", color: "bg-red-400" },
];

export default function EmergentToolUseSim() {
  const [log, setLog] = useState([]);
  const [step, setStep] = useState(0);

  const simulateStep = () => {
    const actions = [
      "O Escondedor move uma caixa para bloquear a entrada",
      "O Procurador tenta saltar pela rampa",
      "O Escondedor usa outra caixa para se esconder",
      "O Procurador tenta empurrar uma caixa para abrir caminho",
    ];
    const next = actions[step % actions.length];
    setLog((prev) => [...prev, next]);
    setStep((prev) => prev + 1);
  };

  return (
    <div className="p-4 max-w-2xl mx-auto space-y-4">
      <h1 className="text-2xl font-bold text-center">Simulação de Uso Emergente de Ferramentas</h1>

      <div className="grid grid-cols-2 gap-4">
        {agents.map((agent) => (
          <motion.div
            key={agent.id}
            className={`rounded-2xl p-4 shadow-lg ${agent.color} text-white text-center`}
            initial={{ opacity: 0, y: 20 }}
            animate={{ opacity: 1, y: 0 }}
            transition={{ duration: 0.5 }}
          >
            {agent.name}
          </motion.div>
        ))}
      </div>

      <Card>
        <CardContent className="p-4">
          <h2 className="text-xl font-semibold mb-2">Ações da Simulação</h2>
          <div className="space-y-2 max-h-60 overflow-y-auto">
            {log.map((entry, idx) => (
              <div key={idx} className="text-sm">{entry}</div>
            ))}
          </div>
          <Button onClick={simulateStep} className="mt-4 w-full">
            Executar Próxima Ação
          </Button>
        </CardContent>
      </Card>
    </div>
  );
}

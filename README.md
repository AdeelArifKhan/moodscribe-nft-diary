import { useState } from "react";
import { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Textarea } from "@/components/ui/textarea";

export default function MoodScribe() {
  const [mood, setMood] = useState("");
  const [diary, setDiary] = useState("");
  const [image, setImage] = useState(null);
  const [loading, setLoading] = useState(false);

  const handleGenerate = async () => {
    setLoading(true);

    // Generate diary entry using OpenAI (placeholder)
    const diaryEntry = `Today I felt ${mood}. It was a day of reflection and emotion.`;
    setDiary(diaryEntry);

    // Placeholder image generation
    setImage("https://via.placeholder.com/400x200.png?text=" + mood);

    setLoading(false);
  };

  const handleMint = async () => {
    alert("Minting to Solana... (feature under development)");
  };

  return (
    <div className="p-6 max-w-xl mx-auto">
      <h1 className="text-2xl font-bold mb-4">MoodScribe - Emotion NFT Diary</h1>

      <Card className="mb-4">
        <CardContent className="space-y-4">
          <Input
            placeholder="Enter your mood (e.g., happy, anxious)"
            value={mood}
            onChange={(e) => setMood(e.target.value)}
          />
          <Button onClick={handleGenerate} disabled={loading}>
            {loading ? "Generating..." : "Generate Diary Entry"}
          </Button>
        </CardContent>
      </Card>

      {diary && (
        <Card className="mb-4">
          <CardContent>
            <h2 className="text-xl font-semibold mb-2">Generated Entry</h2>
            <Textarea rows={4} value={diary} readOnly />
          </CardContent>
        </Card>
      )}

      {image && (
        <Card className="mb-4">
          <CardContent>
            <img src={image} alt="Mood Art" className="rounded" />
          </CardContent>
        </Card>
      )}

      {diary && image && (
        <Button onClick={handleMint}>Mint as NFT on Solana</Button>
      )}
    </div>
  );
}

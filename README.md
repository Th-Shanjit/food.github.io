import React, { useState } from 'react';
import { Clock, Users, ChefHat, Printer, CheckCircle2, Circle, Utensils, Flame } from 'lucide-react';

const RECIPE_META = {
  title: "Dada Boudi Chicken Biryani",
  prepTime: "20 Mins",
  cookTime: "50 Mins",
  totalTime: "1 Hr 10 Mins",
  servings: "4-6",
  cuisine: "Bengali / Indian"
};

const INGREDIENTS = [
  {
    category: "Special Biryani Garam Masala",
    items: [
      "1 tsp Shahi Jeera (Caraway seeds)",
      "1 tsp Whole Coriander Seeds",
      "1 tsp White Peppercorns (Shamorich)",
      "5 Green Cardamoms & 2 Black Cardamoms",
      "4 Cloves & 2 Cinnamon sticks",
      "1 Mace (Javitri)",
      "1 small piece of Nutmeg"
    ]
  },
  {
    category: "Chicken & Potatoes (The Gravy)",
    items: [
      "1.5 kg Chicken (Cut into large 250g pieces)",
      "6 Large Potatoes (Peeled)",
      "400g Onions (Thinly sliced)",
      "3 cloves Garlic & 15g Ginger (Blended with a little water)",
      "150g Sour Yogurt (Curd)",
      "10 Aloo Bukhara (Dried Plums)",
      "200 ml Refined White Oil & 1 tsp Ghee",
      "2 tsp Kashmiri Red Chili Powder & 1 tsp Turmeric Powder",
      "2 drops Meetha Attar (Sweet Kewra essence)",
      "Salt to taste"
    ]
  },
  {
    category: "For the Rice",
    items: [
      "1 kg Basmati Rice",
      "Whole spices: 2 Bay Leaves, 2 Cinnamon sticks, 5 Black Peppercorns, 4 Cloves",
      "Salt to taste"
    ]
  },
  {
    category: "For Layering (Flavorings)",
    items: [
      "200 ml Buffalo Milk (or Cow's Milk)",
      "50g Khoya (Mawa)",
      "1/2 tsp Cardamom Powder",
      "2 cups Water",
      "1 tsp Rose Water & 2 tsp Kewra Water",
      "2 drops Meetha Attar",
      "1/2 tsp Saffron (Kesar)",
      "3 tsp Ghee"
    ]
  },
  {
    category: "Green Chutney (Accompaniment)",
    items: [
      "Fresh Coriander Leaves & Fresh Mint Leaves (2:1 ratio)",
      "5-6 Green Chilies & 2-3 small pieces of Ginger",
      "2 cloves Garlic",
      "Juice of 1/2 Lemon",
      "1/2 tsp Black Salt (Kala Namak) & 1 tsp Chaat Masala",
      "3 tsp Sour Yogurt",
      "Regular Salt to taste"
    ]
  }
];

const INSTRUCTIONS = [
  {
    title: "Prep the Masala & Chicken",
    steps: [
      "Lightly dry roast all the 'Special Biryani Garam Masala' ingredients in a pan on low heat. Once fragrant and cooled, grind them into a fine powder.",
      "Make small slits in the large chicken pieces with a knife so the spices can penetrate deep inside."
    ]
  },
  {
    title: "Prepare the Gravy & Potatoes",
    steps: [
      "Heat 200 ml white oil and 1 tsp ghee in a large heavy-bottomed pot. Add the sliced onions and fry on high heat for 10-15 minutes until golden brown.",
      "Add some water, salt, Kashmiri chili powder, and turmeric. Stir well. Add the potatoes, more water to submerge them, and 2 drops of Meetha Attar for aroma.",
      "Add the ginger-garlic water. Cover and cook until the potatoes are 80% done. Carefully remove only the potatoes with a slotted spoon and set them aside. Leave the onion gravy in the pot."
    ]
  },
  {
    title: "Cook the Chicken",
    steps: [
      "Add the chicken pieces to the remaining onion gravy along with salt. Do not add extra water (the chicken will release its own juices). Cover and cook for 7-8 minutes.",
      "The chicken should be 60% cooked and the oil should separate. (Note: For 1kg of rice, you want about 500ml of this rich gravy remaining in the pot).",
      "Arrange the par-cooked potatoes and chicken evenly at the bottom of the pot. Toss in the 10 Aloo Bukhara. Spread 150g of beaten yogurt and 2 tsp of your prepared Garam Masala over the top."
    ]
  },
  {
    title: "Prepare the Flavorings",
    steps: [
      "In a bowl, mix the milk, grated Khoya, and cardamom powder together.",
      "In another bowl, combine the 2 cups of water, rose water, kewra water, saffron, and 2 drops of Meetha Attar."
    ]
  },
  {
    title: "Cook the Rice",
    steps: [
      "Wash the Basmati rice 3-4 times until the water runs completely clear, then soak it.",
      "Boil a large pot of water with the bay leaves, cinnamon, peppercorns, cloves, and salt. Once boiling, gently add the soaked rice."
    ]
  },
  {
    title: "Layering & Dum (Steaming)",
    steps: [
      "When the rice is 60% cooked, use a strainer to transfer half of it directly over the chicken and potatoes. Spread it evenly. Pour the milk & khoya mixture over this layer.",
      "Add the remaining rice on top. Pour the saffron water evenly over the rice. Sprinkle 3 tsp of ghee and a pinch of the leftover Garam Masala on top.",
      "Cover the pot tightly with aluminum foil (splash a few drops of water on the rim to help it stick) and place a heavy lid on top.",
      "Place the sealed pot on a hot Tawa (flat griddle). Cook on high heat for 10 minutes, lower the flame to the lowest setting for 15 minutes, then turn off the heat completely and let it rest undisturbed for 10 minutes."
    ]
  },
  {
    title: "Make the Green Chutney & Serve",
    steps: [
      "Blend the coriander, mint, green chilies, ginger, garlic, lemon juice, black salt, regular salt, chaat masala, yogurt, and a tiny splash of water in a mixer until smooth.",
      "Carefully open the foil—the aroma will be incredible! Gently cut through the layers with a spatula, lifting the rich masala chicken from the bottom alongside the fragrant white and yellow rice. Serve piping hot with the fresh Green Chutney!"
    ]
  }
];

export default function App() {
  const [checkedItems, setCheckedItems] = useState(new Set());
  const [imgError, setImgError] = useState(false);

  const toggleCheck = (item) => {
    const newChecked = new Set(checkedItems);
    if (newChecked.has(item)) {
      newChecked.delete(item);
    } else {
      newChecked.add(item);
    }
    setCheckedItems(newChecked);
  };

  const handlePrint = () => {
    window.print();
  };

  return (
    <div className="min-h-screen bg-stone-100 sm:py-8 sm:px-4 md:px-8 font-sans text-stone-800">
      <div className="max-w-5xl mx-auto bg-white sm:rounded-3xl shadow-none sm:shadow-xl overflow-hidden print:shadow-none">
        
        {/* Header Section */}
        <div className="relative h-72 sm:h-80 md:h-96 w-full bg-stone-800">
          {!imgError ? (
            <img 
              src="https://images.unsplash.com/photo-1563379091339-03b21ab4a4f8?ixlib=rb-1.2.1&auto=format&fit=crop&w=1600&q=80" 
              alt="Delicious Biryani" 
              className="w-full h-full object-cover opacity-80"
              onError={() => setImgError(true)}
            />
          ) : (
            <div className="w-full h-full bg-orange-900 opacity-80 flex items-center justify-center">
              <Utensils className="w-24 h-24 text-orange-200 opacity-50" />
            </div>
          )}
          <div className="absolute inset-0 bg-gradient-to-t from-stone-900 via-stone-900/60 sm:via-stone-900/40 to-transparent"></div>
          
          <div className="absolute bottom-0 left-0 w-full p-5 sm:p-10 text-white">
            <h1 className="text-3xl sm:text-5xl font-bold mb-4 text-orange-50 leading-tight tracking-tight">{RECIPE_META.title}</h1>
            
            <div className="grid grid-cols-2 sm:flex sm:flex-wrap gap-y-3 gap-x-4 sm:gap-8 text-sm sm:text-base font-medium text-orange-100">
              <div className="flex items-center gap-2">
                <Clock className="w-4 h-4 sm:w-5 sm:h-5 text-orange-400" />
                <span>Prep: {RECIPE_META.prepTime}</span>
              </div>
              <div className="flex items-center gap-2">
                <Flame className="w-4 h-4 sm:w-5 sm:h-5 text-orange-400" />
                <span>Cook: {RECIPE_META.cookTime}</span>
              </div>
              <div className="flex items-center gap-2">
                <Users className="w-4 h-4 sm:w-5 sm:h-5 text-orange-400" />
                <span>Serves: {RECIPE_META.servings}</span>
              </div>
              <div className="flex items-center gap-2">
                <ChefHat className="w-4 h-4 sm:w-5 sm:h-5 text-orange-400" />
                <span className="truncate">{RECIPE_META.cuisine}</span>
              </div>
            </div>
          </div>

          <button 
            onClick={handlePrint}
            className="absolute top-4 right-4 sm:top-6 sm:right-6 bg-black/20 hover:bg-black/40 backdrop-blur-md text-white p-2.5 sm:p-3 rounded-full transition-all print:hidden active:scale-95"
            title="Print Recipe"
          >
            <Printer className="w-5 h-5 sm:w-6 sm:h-6" />
          </button>
        </div>

        {/* Main Content Area */}
        <div className="p-5 sm:p-10 grid grid-cols-1 lg:grid-cols-12 gap-8 sm:gap-10">
          
          {/* Ingredients Column */}
          <div className="lg:col-span-4 space-y-6 sm:space-y-8 bg-stone-50 p-5 sm:p-8 rounded-2xl border border-stone-200 print:border-none print:p-0 print:bg-transparent">
            <h2 className="text-xl sm:text-2xl font-bold text-stone-800 flex items-center gap-3 border-b border-stone-200 pb-3 sm:pb-4 sticky top-0 bg-stone-50 z-10 print:static pt-2 sm:pt-0">
              <Utensils className="w-5 h-5 sm:w-6 sm:h-6 text-orange-600" />
              Ingredients
            </h2>
            
            <div className="space-y-6">
              {INGREDIENTS.map((section, idx) => (
                <div key={idx}>
                  <h3 className="text-base sm:text-lg font-semibold text-orange-800 mb-2 sm:mb-3">{section.category}</h3>
                  <ul className="space-y-1 sm:space-y-2">
                    {section.items.map((item, itemIdx) => {
                      const isChecked = checkedItems.has(item);
                      return (
                        <li 
                          key={itemIdx}
                          onClick={() => toggleCheck(item)}
                          className={`flex items-start gap-3 cursor-pointer group transition-all duration-300 ease-out p-2 -mx-2 rounded-xl active:bg-stone-200 sm:hover:bg-stone-100 print:break-inside-avoid print:p-0 print:mx-0
                            ${isChecked ? 'text-stone-400 opacity-60' : 'text-stone-700'}`}
                        >
                          <div className="mt-0.5 flex-shrink-0 text-orange-500 transition-transform duration-300 group-active:scale-90">
                            {isChecked ? (
                              <CheckCircle2 className="w-5 h-5 text-green-500 transition-all duration-300" />
                            ) : (
                              <Circle className="w-5 h-5 transition-all duration-300" />
                            )}
                          </div>
                          <span className={`text-sm sm:text-base leading-relaxed transition-all duration-300 ${isChecked ? 'line-through decoration-stone-300' : ''}`}>
                            {item}
                          </span>
                        </li>
                      );
                    })}
                  </ul>
                </div>
              ))}
            </div>
          </div>

          {/* Instructions Column */}
          <div className="lg:col-span-8 space-y-6 sm:space-y-8">
            <h2 className="text-xl sm:text-2xl font-bold text-stone-800 flex items-center gap-3 border-b border-stone-200 pb-3 sm:pb-4 sticky top-0 bg-white z-10 print:static pt-2 sm:pt-0">
              <ChefHat className="w-5 h-5 sm:w-6 sm:h-6 text-orange-600" />
              Instructions
            </h2>

            <div className="space-y-8 sm:space-y-10">
              {INSTRUCTIONS.map((section, idx) => (
                <div key={idx} className="print:break-inside-avoid">
                  <h3 className="text-lg sm:text-xl font-bold text-stone-800 mb-3 sm:mb-4 flex items-start sm:items-center gap-3">
                    <span className="flex items-center justify-center flex-shrink-0 w-7 h-7 sm:w-8 sm:h-8 mt-0.5 sm:mt-0 rounded-full bg-orange-100 text-orange-700 text-xs sm:text-sm font-bold shadow-sm">
                      {idx + 1}
                    </span>
                    <span className="leading-tight">{section.title}</span>
                  </h3>
                  
                  <div className="space-y-4 sm:pl-11 pl-10">
                    {section.steps.map((step, stepIdx) => (
                      <p key={stepIdx} className="text-stone-600 leading-relaxed text-sm sm:text-lg">
                        {step}
                      </p>
                    ))}
                  </div>
                </div>
              ))}
            </div>

            {/* Print Note */}
            <div className="mt-8 sm:mt-12 p-5 sm:p-6 bg-orange-50 rounded-2xl border border-orange-100 text-orange-800 text-center print:hidden shadow-sm">
              <p className="font-semibold text-sm sm:text-base">Ready to start cooking?</p>
              <p className="text-xs sm:text-sm mt-1.5 opacity-80">Tap the ingredients on your screen to check them off as you prep!</p>
            </div>
          </div>
        </div>
        
      </div>
    </div>
  );
}

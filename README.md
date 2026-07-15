// Step 1: Initial Skills Array
const rawSkills = [" javascript ", "REACT", "node.js ", "", "  PYTHON  "];

// Step 2: Clean and Uppercase with map()
const cleanedSkills = rawSkills.map(skill => skill.trim().toUpperCase());
console.log("cleanedSkills :", cleanedSkills);

// Step 3: Filter Empty Skills with filter()
const validSkills = cleanedSkills.filter(skill => skill !== "");
console.log("validSkills :", validSkills);

// Step 4: Count Valid Skills with reduce()
const totalSkillCount = validSkills.reduce((count, skill) => count + 1, 0);
console.log("totalSkillCount :", totalSkillCount);

// Step 5: Sort Skills Alphabetically
const sortedSkills = validSkills.sort();
console.log("sortedSkills :", sortedSkills);

// Step 6: Group Skills by First Letter with reduce()
const groupedByFirstLetter = sortedSkills.reduce((groups, skill) => {
  const firstLetter = skill[0];
  if (!groups[firstLetter]) {
    groups[firstLetter] = [];
  }
  groups[firstLetter].push(skill);
  return groups;
}, {});

console.log("grouped by first letter :", groupedByFirstLetter);

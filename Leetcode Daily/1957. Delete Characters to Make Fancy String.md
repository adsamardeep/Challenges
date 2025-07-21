class Solution:
    def makeFancyString(self, s: str) -> str:
        # Step 1: If the string is too short, return as-is
        if len(s) < 3:
            return s

        # Step 2: Create result string
        result = s[0]

        # Step 3: First character is already added
        # Step 4: Initialize repeat count
        count = 1

        # Step 5: Loop through rest of the characters
        for i in range(1, len(s)):
            if s[i] == s[i - 1]:
                # Increase count if same as previous
                count += 1
            else:
                # Reset count if different
                count = 1

            # Step 6: Add to result only if count < 3
            if count < 3:
                result += s[i]

        # Step 7: Return the fancy string
        return result
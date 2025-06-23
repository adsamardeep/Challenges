class Solution:
    def kMirror(self, k: int, n: int) -> int:
        def is_base_k_palindrome(num: int, k: int) -> bool:
            # Step 4: Convert to base-k and reverse
            original = num
            reversed_num = 0
            while num > 0:
                reversed_num = reversed_num * k + num % k
                num //= k
            return original == reversed_num

        def create_palindrome(half: int, odd: bool) -> int:
            # Step 3: Create full decimal palindrome from half
            pal = half
            if odd:
                half //= 10  # Drop last digit for odd-length palindromes
            while half > 0:
                pal = pal * 10 + half % 10
                half //= 10
            return pal

        sum_ = 0      # Step 1: Initialize sum
        found = 0     # Step 1: Initialize count
        length = 1    # Start with palindromes of length 1

        # Step 2: Continue until we find n valid numbers
        while found < n:
            start = 10 ** ((length - 1) // 2)
            end = 10 ** ((length + 1) // 2)

            # Step 3: Generate palindromes
            for half in range(start, end):  
                pal = create_palindrome(half, length % 2 == 1)
                # Step 4: Check base-k palindromicity
                if is_base_k_palindrome(pal, k):  
                    # Step 5: Add to sum
                    sum_ += pal        
                    found += 1
                    # Step 6: If enough numbers found, return
                    if found == n:     
                        return sum_
            # Step 7: Final Return
            length += 1  

        return sum_
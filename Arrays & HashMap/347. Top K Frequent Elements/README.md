class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        HashMap<Integer,Integer> map = new HashMap<>();

        for(int num:nums){
            map.put(num, map.getOrDefault(num,0)+1);
        }

          // Create a list of lists to bucket elements by frequency
        ArrayList<List<Integer>> count = new ArrayList<>();
        for (int i = 0; i <= nums.length; i++) {
            count.add(new ArrayList<>());
        }


        for(int key : map.keySet()){
            int freq = map.get(key);
            count.get(freq).add(key);
            
        }
        
        List<Integer> res= new ArrayList<>();
        for(int i=count.size()-1;i>=0;i--){
            if(count.get(i)!=null){
                res.addAll(count.get(i));
            }
            
            if(res.size()>=k) break;
        }
        int h[] = new int[k];

        for(int i=0;i<k;i++){
            h[i]= res.get(i);
        }

        return h;
    }
}

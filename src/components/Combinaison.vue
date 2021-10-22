<template>

</template>

<script>
export default {

setup() {

    // pseudo code
// debut denombrement_combinaisons( k , n ) {
//  si (k = n) retourner 1;
//  si (k > n/2) k = n-k;
//  res = n-k+1;
//  pour i = 2 par 1 tant que i < = k
//   res = res * (n-k+i)/i;
//  fin pour
//  retourner res;
// fin
// // langage C
// double factorielle(double x) {
//  double i;
//  double result=1;
//  if (x >= 0) {
//   for(i=x;i>1;i--) {
//    result = result*i;
//   }
//   return result;
//  }
//  return 0; // erreur
// }
// double compter_combinaisons(double x,double y) {
//  double z = x-y;
//  return factorielle(x)/(factorielle(y)*factorielle(z));
// }<code><br>// Langage VBA<br>Function Factorielle(n As Integer) As Double<br> Factorielle = 1<br> For i = 1 To n<br>  Factorielle = Factorielle * i<br> Next<br>End Function<br>Function NbCombinaisons (k As Integer, n As Integer) As Double<br> Dim z As Integer<br> z = n - k<br> NbCombinaisons = Factorielle(n) / (Factorielle(k) * Factorielle(z))<br>End Function<br></code>

    // javascript
function combinaisons(a) { // a = new Array(1,2)
  var fn = function(n, source, en_cours, tout) {
    if (n == 0) {
      if (en_cours.length > 0) {
        tout[tout.length] = en_cours;
      }
      return;
    }
    for (var j = 0; j < source.length; j++) {
      fn(n - 1, source.slice(j + 1), en_cours.concat([source[j]]), tout);
    }
    return;
  }
  var tout = [];
  for (var i=0; i < a.length; i++) {
    fn(i, a, [], tout);
  }
  tout.push(a);
  return tout;
}
}
}
</script>

<style>

</style>

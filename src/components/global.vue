
<script>
 
 import crypto from 'crypto'

 function shade(any, dg) {
    const hash = crypto.createHash('sha256','utf-8').update(any).digest(dg);
    return hash;
 }


export default {
    name: 'global',
    shade
}
</script>
canvas-daviferreira-png-transparente
====================================

Forçar o PNG transparente


Uso a classe Canvas faz algum tempo com ZF e hoje tive problemas com a transparência de imagens png. 
Uma correção que me ajudou e solucionou meu problema com png transparente.

Ao usar a função resize() era certo que ficava preto o fundo e quando não usava a função resize() alguns png 
mantiam o fundo transparente e outros ficavam cinzas ou pretos também.

Bom depois da pesquisa no Google adicionei o seguinte código na função output_image()

ficou assim:

  private function output_image($destination = null){
    $pathinfo = pathinfo($destination);
    $extension = ($pathinfo["extension"] ? strtolower($pathinfo["extension"]) : $this->extension);
	
	
    if($extension == "jpg" || $extension =="jpeg" || $extension == "bmp"){
    	imagejpeg($this->image, $destination, $this->quality);
    } elseif($extension == "png"){
		imagealphablending( $this->image, false ); // aqui 
		imagesavealpha( $this->image, true ); // aqui
    	imagepng($this->image, $destination);
    } elseif($extension == "gif"){
    	imagegif($this->image, $destination);
    } else{
    	return false;
    }
	
	
	/*
    if($extension == "jpg" || $extension =="jpeg" || $extension == "bmp")
    	imagejpeg($this->image, $destination, $this->quality);
    elseif($extension == "png")
    	imagepng($this->image, $destination);
    elseif($extension == "gif")
    	imagegif($this->image, $destination);
    else
    	return false;
    */
      
  }
  
  Documentação da classe e Download: http://canvas.daviferreira.com/
  
